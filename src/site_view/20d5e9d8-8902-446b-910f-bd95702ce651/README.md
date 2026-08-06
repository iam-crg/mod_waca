### JCB! Site View
# CALPAY Transactions (calpaytransactions)

## HTML:
```html
  <div class="row mb-3">
    <div class="col-md-3">
      <label for="from_date" class="form-label">
        <?php //echo Text::_('COM_CALPAY_FROM_DATE'); 
        echo "From Date";
        ?>
      </label>
      <input
             type="date"
             class="form-control"
             id="from_date"
             name="from_date"
             value="<?php echo htmlspecialchars($this->fromDate, ENT_QUOTES, 'UTF-8'); ?>"
             >
    </div>

    <div class="col-md-3">
      <label for="to_date" class="form-label">
        <?php //echo Text::_('COM_CALPAY_TO_DATE'); 
        echo "To Date";
        ?>
      </label>
      <input
             type="date"
             class="form-control"
             id="to_date"
             name="to_date"
             value="<?php echo htmlspecialchars($this->toDate, ENT_QUOTES, 'UTF-8'); ?>"
             >
    </div>

    <div class="col-md-2 d-flex align-items-end">
      <div class="form-check mb-2">
        <input
               class="form-check-input"
               type="checkbox"
               id="approved_only"
               name="approved_only"
               value="1"
               <?php echo $this->approvedOnly ? 'checked' : ''; ?>
               >
        <label class="form-check-label" for="approved_only">
          Approved only
        </label>
      </div>
    </div>

    <div class="col-md-2 d-flex align-items-end">
      <button type="submit" class="btn btn-primary">
        <?php echo Text::_('JSEARCH_FILTER_SUBMIT'); ?>
      </button>
    </div>
  </div>
  <?php
  $fromDateLabel = !empty($this->fromDate)
    ? \DateTime::createFromFormat('Y-m-d', $this->fromDate)->format('d M Y')
      : '';

  $toDateLabel = !empty($this->toDate)
    ? \DateTime::createFromFormat('Y-m-d', $this->toDate)->format('d M Y')
      : '';
  ?>



  <table class="calpay-table">

    <thead>
    <tr>
         <th colspan="13" class="text-center">
            <h3 class="mb-0">
                Transactions (<?php echo $this->approvedOnly ? 'Approved Only' : 'All'; ?>)
                between
                <?php echo htmlspecialchars($fromDateLabel, ENT_QUOTES, 'UTF-8'); ?>
                and
                <?php echo htmlspecialchars($toDateLabel, ENT_QUOTES, 'UTF-8'); ?>
            </h3>
        </th>
    </tr>
      <tr>
        <th>Response</th>
        <th>User Name</th>
        <th>Transaction ID</th>

        <th style='nowrap'>Date</th>
        <th>Authorization</th>
        <th>Type</th>
        <th>Amount</th>
        <th>Status</th>

        <th>Customer</th>
        <th>Order Description</th>
        <th>Product SKU</th>
        <th>Description</th>
        <th>Quantity</th>

      </tr></thead>
    <tbody>
<?php

if (!empty($this->fromDate) && !empty($this->toDate))
{
    $result = CalpayHelper::getTransactions(
        $this->params,
        $this->fromDate,
        $this->toDate
    );

    if ($result && ($xml = simplexml_load_string($result)) !== false)
    {

        $allTransactions = [];

        $totalAmount = 0;
        $totalQuantity = 0;
        $totalTransactions = 0;


        // Filter transactions first
        foreach ($xml as $tx)
        {
            $isApproved = (
                (string) $tx->action->response_code === '100'
                && (string) $tx->action->success === '1'
            );

            if ($this->approvedOnly && !$isApproved)
            {
                continue;
            }

            $allTransactions[] = $tx;

            $totalTransactions++;
            $totalAmount += (float) $tx->action->amount;
            $totalQuantity += (float) $tx->product->quantity;
        }


        /*
         * Pagination
         */
        $limit = 20;

        $page = Factory::getApplication()
            ->input
            ->getInt('page', 1);

        $totalPages = ceil(count($allTransactions) / $limit);

        $offset = ($page - 1) * $limit;

        $transactionsPage = array_slice(
            $allTransactions,
            $offset,
            $limit
        );


        /*
         * Display transactions
         */
        foreach ($transactionsPage as $tx)
        {

            $isFailed = (
                (string) $tx->action->response_code !== '100'
                || (string) $tx->action->success !== '1'
            );


            echo '<tr class="' . ($isFailed ? 'failed-transaction' : '') . '">';


            echo '<td>' .
                htmlspecialchars(
                    (string)$tx->action->response_code . ' ' .
                    (string)$tx->action->success
                ) .
            '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->action->username) . '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->transaction_id) . '</td>';


            $date = \DateTime::createFromFormat(
                'YmdHis',
                (string)$tx->action->date
            );

            echo '<td>' . ($date ? $date->format('d M Y') : '') . '</td>';


            echo '<td>' . htmlspecialchars((string)$tx->authorization_code) . '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->action->action_type) . '</td>';

            echo '<td>$' .
                number_format((float)$tx->action->amount,2) .
            '</td>';

            echo '<td>' .
                htmlspecialchars((string)$tx->action->response_text) .
            '</td>';

            echo '<td>' .
                htmlspecialchars(
                    (string)$tx->first_name . ' ' .
                    (string)$tx->last_name
                ) .
            '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->order_description) . '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->product->sku) . '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->product->description) . '</td>';

            echo '<td>' . htmlspecialchars((string)$tx->product->quantity) . '</td>';


            echo '</tr>';
        }

?>
<!--
<tfoot>
<tr class="calpay-total-row">
    <td colspan="6" class="text-end">
        <strong>Totals</strong>
    </td>
    <td>
        <strong>
            $<?php echo number_format($totalAmount,2); ?>
        </strong>
    </td>
    <td colspan="5"></td>
    <td>
        <strong>
            <?php echo number_format($totalQuantity,4); ?>
        </strong>
    </td>
</tr>

<tr class="calpay-total-row">
    <td colspan="13" class="text-center">
        <strong>
            <?php echo $totalTransactions; ?> Transactions
        </strong>
    </td>
</tr>
</tfoot>
-->
<?php

    }
}

?>
  </table>
  
  <?php if (!empty($totalPages) && $totalPages > 1): ?>

<nav>
<ul class="pagination justify-content-center">

<?php for ($i = 1; $i <= $totalPages; $i++): ?>

<li class="page-item <?php echo ($page == $i) ? 'active' : ''; ?>">

<a class="page-link"
href="calpay/transactions?from_date=<?php echo $this->fromDate; ?>&to_date=<?php echo $this->toDate; ?>&approved_only=<?php echo $this->approvedOnly; ?>&page=<?php echo $i; ?>">

<?php echo $i; ?>

</a>

</li>

<?php endfor; ?>

</ul>
</nav>

<?php endif; ?>
```

> Deliver dynamic, custom front-end experiences with this reusable Site View crafted for seamless data flow and design flexibility in JCB.

### Used in [Joomla Component Builder](https://www.joomlacomponentbuilder.com) - [Source](https://git.vdm.dev/joomla/Component-Builder) - [Mirror](https://github.com/vdm-io/Joomla-Component-Builder) - [Download](https://git.vdm.dev/joomla/pkg-component-builder/releases)

---
[![Joomla Volunteer Portal](https://img.shields.io/badge/-Joomla-gold?logo=joomla)](https://volunteers.joomla.org/joomlers/1396-llewellyn-van-der-merwe "Join Llewellyn on the Joomla Volunteer Portal: Shaping the Future Together!") [![GitHub](https://img.shields.io/badge/-Git-181717?logo=git)](https://github.com/joomengine "Build premium Joomla extensions with JoomEngine on GitHub: Help us raise Joomla extension standards!") [![Octoleo](https://img.shields.io/badge/-Octoleo-black?logo=linux)](https://git.vdm.dev/octoleo "--quiet") [![Llewellyn](https://img.shields.io/badge/-Llewellyn-ffffff?logo=gitea)](https://git.vdm.dev/Llewellyn "Collaborate and Innovate with Llewellyn on Git: Building a Better Code Future!") [![Telegram](https://img.shields.io/badge/-Telegram-blue?logo=telegram)](https://t.me/Joomla_component_builder "Join Llewellyn and the Community on Telegram: Building Joomla Components Together!") [![Mastodon](https://img.shields.io/badge/-Mastodon-9e9eec?logo=mastodon)](https://joomla.social/@llewellyn "Connect and Engage with Llewellyn on Joomla Social: Empowering Communities, One Post at a Time!") [![X (Twitter)](https://img.shields.io/badge/-X-black?logo=x)](https://x.com/llewellynvdm "Join the Conversation with Llewellyn on X: Where Ideas Take Flight!") [![GitHub](https://img.shields.io/badge/-GitHub-181717?logo=github)](https://github.com/Llewellynvdm "Build, Innovate, and Thrive with Llewellyn on GitHub: Turning Ideas into Impact!") [![YouTube](https://img.shields.io/badge/-YouTube-ff0000?logo=youtube)](https://www.youtube.com/@OctoYou "Explore, Learn, and Create with Llewellyn on YouTube: Your Gateway to Inspiration!") [![n8n](https://img.shields.io/badge/-n8n-black?logo=n8n)](https://n8n.io/creators/octoleo "Effortless Automation and Impactful Workflows with Llewellyn on n8n!") [![Docker Hub](https://img.shields.io/badge/-Docker-grey?logo=docker)](https://hub.docker.com/r/octoleo/joomengine "JoomEngine on Docker: Containerize Your Creativity!") [![Open Collective](https://img.shields.io/badge/-Donate-green?logo=opencollective)](https://opencollective.com/joomla-component-builder "Donate towards JCB: Help Llewellyn financially so he can continue developing this great tool!") [![GPG Key](https://img.shields.io/badge/-GPG-blue?logo=gnupg)](https://git.vdm.dev/Llewellyn/gpg "Unlock Trust and Security with Llewellyn's GPG Key: Your Gateway to Verified Connections!")