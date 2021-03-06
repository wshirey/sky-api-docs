---
layout: layout-sidebar
name: Treasury
description: Information on additions and changes for the Treasury API.
order: 225
published: true
showInNav: true
icon: fa fa-money
back_to_top: true
title: Treasury Changelog
---

# {{ name }}

Monitor this page to keep up with the [Treasury API]({{ stache.config.portal_endpoints_treasury }}) latest changes and {{ stache.config.api_type_name }} service releases.

## 2018-07-11

### Announcement: Changes for [Treasury API]({{ stache.config.portal_endpoints_treasury }})

We will transition the [Treasury (Beta)]({{ stache.config.portal_endpoints_treasury }}) API out of its current public beta phase and into a formal v1 release.

## June

### 2018-06-28

#### New

Added the following endpoint:

<div class="table-responsive">
	<table class="table table-striped table-hover">
		<thead>
			<tr>
				<th>Operation</th>
				<th>Method</th>
				<th>Route</th>
			</tr>
		</thead>
		<tbody>
			<tr class="clickable-row" data-url="{{ stache.config.portal_endpoints_transaction_code_list_treasury }}">
				<td>Transaction code (List)</td>
				<td>GET</td>
				<td>/transactioncodes</td>
			</tr>
		</tbody>
		<tbody>
			<tr class="clickable-row" data-url="{{ stache.config.portal_endpoints_transaction_code_value_list_treasury }}">
				<td>Transaction code value (List)</td>
				<td>GET</td>
				<td>/transactioncodes/{transaction_code_id}/value</td>
			</tr>
		</tbody>
	</table>
</div>

These endpoints currently exist in the General Ledger API. We decided to include them in the Treasury API (and Accounts Payable API) because values from those endpoints may be required to create Treasury (or Accounts Payable) records.

#### Changed

We fixed an issue for [Deposit (Get)]({{ stache.config.portal_endpoints_deposit_get }}) to set the `name` in `transaction_code_values` in `distribution_splits`.

### 2018-06-12

#### Announcement: Changes for [Treasury API]({{ stache.config.portal_endpoints_treasury }})

We implemented new operation ID values in the OpenApi (fka Swagger) definitions for all endpoints in the Treasury API. Note that any existing code relying on these endpoints will continue to function, since all routes and parameters are unchanged. However, if you make use of client-side generated code and want to regenerate your client wrapper, compile-time errors in your code stemming from new operation ID values will arise and need to be addressed.

### 2018-06-04

#### Announcement: Changes Planned for [Accounts Payable]({{ stache.config.portal_endpoints_AP }}), [General Ledger]({{ stache.config.portal_endpoints_GL }}), and [Treasury]({{ stache.config.portal_endpoints_treasury }}) APIs

We will implement new operation ID values in the OpenApi (fka Swagger) definitions for several SKY APIs. This change will improve client-side tooling support for code generation by making these values more deterministic and friendlier across different languages. Going forward, we expect high stability of these values (meaning, we won’t need to change them again).

Note that any existing code that has been deployed will continue to function with no problems, since we are not changing any routes or parameters. If you make use of client-side generated code and want to regenerate your client wrapper, you’ll need to fix any compile-time errors in your code stemming from new method names.

## April

### 2018-04-26

#### Changed

- For the  [Bank account (List)]({{ stache.config.portal_endpoints_bank_account_list }}) endpoint, the `bank_name` field is now included in the list of returned objects separate from `account_name`.
- The  [Bank account register (List)]({{ stache.config.portal_endpoints_bank_account_register_list }}), [Checks (List)]({{ stache.config.portal_endpoints_checks_list }}), [Deposits (List)]({{ stache.config.portal_endpoints_deposits_list }}), and [Adjustments (List)]({{ stache.config.portal_endpoints_adjustments_list }}) endpoints now return the `transaction_id` field. This field helps to ensure that "register" items correctly map to checks, deposits, and adjustments.

## January

### 2018-01-17

#### Changed

For the  [Checks (List)]({{ stache.config.portal_endpoints_checks_list }}) endpoint, we made the following changes:

- The new `payee` field is now returned in the listed objects.
- The list is now sorted by check number (ascending).
- We added the `starting_check_number` and `ending_check_number` variables to the check filter. When only `starting_check_number` is provided, a list of checks (starting with that number and higher) is returned. When only `ending_check_number` is provided, a list of checks (less than or equal to that number) is returned. When both variables are provided, a range of checks is returned.

## 2017

### 2017-04-25

#### New

The Treasury API has been released for a public beta. This API handles information related to bank accounts, including related entities such as adjustments, checks, and deposits.

The initial release contains endpoints to retrieve a list of all bank accounts and all bank account transactions, and to manage deposits, cash receipts, and adjustments. For more information, check out the [entity]({{ stache.config.treasury_entity_reference }}) and [endpoint]({{ stache.config.portal_endpoints_treasury }}) references.
