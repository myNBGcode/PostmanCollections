# Use case scenario
#### Welcome to the Accounts Sandbox API.

------------------------------------------------------------------------------------------

### The API
This API provides a standard RESTful interface that enables a user to
* Get all their public accounts
* Get all their private accounts
* Get the full details of a specific account

> Visit https://developer.nbg.gr/documentation/Accounts-API-OAuth2-v1.3
> for the full API documentation

### Real life Use Case Scenario

The main functionality of the application is to aggregate financial data for the accounts of a user.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/sandbox/obpaccount/oauth2/v1.3/sandbox

With a request body:
```
 {
   "sandbox_id": "28E82EA8-757C-40B6-BB14-A798893806BD"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**

There exists an application, "Switch", that users can stream online content and accept donations from their viewers. The application needs to give the viewer the ability to 
execute such donations using any of their accounts.

For a viewer to get their accounts in order to select the desired one, the application will make a **HTTP GET** request to the following endpoint:
> https://apis.nbg.gr/sandbox/obpaccount/oauth2/v1.3/obp/banks/{bank_id}/accounts/{account_id}/{view_id}/account

to get the following response:
```json
{
    "id": "8d651bdb-c5a9-4349-84f0-a84913379164",
    "label": "SandboxNBG",
    "number": "97226400154",
    "owners": [
        {
            "id": "79ecc67f-96a4-45ae-9581-b4c91ccc2219",
            "provider": "local",
            "display_name": "sDoulfis"
        }
    ],
    "type": "CURRENT",
    "value": {
        "currency": "EUR",
        "amount": "98999"
    },
    "IBAN": "GR0901109720000097226400154",
    "swift_bic": "ETHNGRAA",
    "bank_id": "DB173089-A8FE-43F1-8947-F1B2A8699829",
    "views_available": [
        {
            "is_public": false,
            "id": "owner",
            "short_name": "owner",
            "description": "owner view",
            "alias": "",
            "hide_metadata_if_alias_used": true,
            "can_add_comment": true,
            "can_add_corporate_location": true,
            "can_add_image": true,
            "can_add_image_url": true,
            "can_add_more_info": true,
            "can_add_open_corporates_url": true,
            "can_add_physical_location": true,
            "can_add_private_alias": true,
            "can_add_public_alias": true,
            "can_add_tag": true,
            "can_add_url": true,
            "can_add_counterparty": true,
            "can_add_where_tag": true,
            "can_add_narrative": true,
            "can_delete_comment": true,
            "can_delete_corporate_location": true,
            "can_delete_image": true,
            "can_delete_physical_location": true,
            "can_delete_tag": true,
            "can_delete_where_tag": true,
            "can_delete_narrative": true,
            "can_delete_image_url": true,
            "can_delete_public_alias": true,
            "can_delete_private_alias": true,
            "can_delete_more_info": true,
            "can_delete_open_corporates_url": true,
            "can_delete_url": true,
            "can_edit_owner_comment": true,
            "can_edit_where_tag": true,
            "can_edit_narrative": true,
            "can_edit_image_url": true,
            "can_edit_public_alias": true,
            "can_edit_private_alias": true,
            "can_edit_physical_location": true,
            "can_edit_corporate_location": true,
            "can_edit_more_info": true,
            "can_edit_open_corporates_url": true,
            "can_edit_url": true,
            "can_see_bank_account_balance": true,
            "can_see_bank_account_bank_name": true,
            "can_see_bank_account_currency": true,
            "can_see_bank_account_iban": true,
            "can_see_bank_account_label": true,
            "can_see_bank_account_national_identifier": true,
            "can_see_bank_account_number": true,
            "can_see_bank_account_owners": true,
            "can_see_bank_account_swift_bic": true,
            "can_see_bank_account_type": true,
            "can_see_comments": true,
            "can_see_narrative": true,
            "can_see_corporate_location": true,
            "can_see_image_url": true,
            "can_see_images": true,
            "can_see_more_info": true,
            "can_see_open_corporates_url": true,
            "can_see_other_account_bank_name": true,
            "can_see_other_account_iban": true,
            "can_see_other_account_kind": true,
            "can_see_other_account_metadata": true,
            "can_see_other_account_national_identifier": true,
            "can_see_other_account_number": true,
            "can_see_other_account_swift_bic": true,
            "can_see_owner_comment": true,
            "can_see_physical_location": true,
            "can_see_private_alias": true,
            "can_see_public_alias": true,
            "can_see_tags": true,
            "can_see_transaction_amount": true,
            "can_see_transaction_balance": true,
            "can_see_transaction_currency": true,
            "can_see_transaction_description": true,
            "can_see_transaction_finish_date": true,
            "can_see_transaction_metadata": true,
            "can_see_transaction_other_bank_account": true,
            "can_see_transaction_start_date": true,
            "can_see_transaction_this_bank_account": true,
            "can_see_transaction_type": true,
            "can_see_url": true,
            "can_see_where_tag": true,
            "can_see_bank_routing_scheme": true,
            "can_see_bank_routing_address": true,
            "can_see_bank_account_routing_scheme": true,
            "can_see_bank_account_routing_address": true,
            "can_see_other_bank_routing_scheme": true,
            "can_see_other_bank_routing_address": true,
            "can_see_other_account_routing_scheme": true,
            "can_see_other_account_routing_address": true
        },
        {
            "is_public": true,
            "id": "publicViewUser1",
            "short_name": "publicView",
            "description": "public view",
            "alias": "",
            "hide_metadata_if_alias_used": false,
            "can_add_comment": false,
            "can_add_corporate_location": false,
            "can_add_image": false,
            "can_add_image_url": false,
            "can_add_more_info": false,
            "can_add_open_corporates_url": false,
            "can_add_physical_location": false,
            "can_add_private_alias": false,
            "can_add_public_alias": false,
            "can_add_tag": false,
            "can_add_url": false,
            "can_add_counterparty": false,
            "can_add_where_tag": false,
            "can_add_narrative": false,
            "can_delete_comment": false,
            "can_delete_corporate_location": false,
            "can_delete_image": false,
            "can_delete_physical_location": false,
            "can_delete_tag": false,
            "can_delete_where_tag": false,
            "can_delete_narrative": false,
            "can_delete_image_url": false,
            "can_delete_public_alias": false,
            "can_delete_private_alias": false,
            "can_delete_more_info": false,
            "can_delete_open_corporates_url": false,
            "can_delete_url": false,
            "can_edit_owner_comment": false,
            "can_edit_where_tag": false,
            "can_edit_narrative": false,
            "can_edit_image_url": false,
            "can_edit_public_alias": false,
            "can_edit_private_alias": false,
            "can_edit_physical_location": false,
            "can_edit_corporate_location": false,
            "can_edit_more_info": false,
            "can_edit_open_corporates_url": false,
            "can_edit_url": false,
            "can_see_bank_account_balance": false,
            "can_see_bank_account_bank_name": false,
            "can_see_bank_account_currency": false,
            "can_see_bank_account_iban": false,
            "can_see_bank_account_label": false,
            "can_see_bank_account_national_identifier": false,
            "can_see_bank_account_number": false,
            "can_see_bank_account_owners": false,
            "can_see_bank_account_swift_bic": false,
            "can_see_bank_account_type": false,
            "can_see_comments": false,
            "can_see_narrative": false,
            "can_see_corporate_location": false,
            "can_see_image_url": false,
            "can_see_images": false,
            "can_see_more_info": false,
            "can_see_open_corporates_url": false,
            "can_see_other_account_bank_name": false,
            "can_see_other_account_iban": false,
            "can_see_other_account_kind": false,
            "can_see_other_account_metadata": false,
            "can_see_other_account_national_identifier": false,
            "can_see_other_account_number": false,
            "can_see_other_account_swift_bic": false,
            "can_see_owner_comment": false,
            "can_see_physical_location": false,
            "can_see_private_alias": false,
            "can_see_public_alias": false,
            "can_see_tags": false,
            "can_see_transaction_amount": false,
            "can_see_transaction_balance": false,
            "can_see_transaction_currency": false,
            "can_see_transaction_description": false,
            "can_see_transaction_finish_date": false,
            "can_see_transaction_metadata": false,
            "can_see_transaction_other_bank_account": false,
            "can_see_transaction_start_date": false,
            "can_see_transaction_this_bank_account": false,
            "can_see_transaction_type": false,
            "can_see_url": false,
            "can_see_where_tag": false,
            "can_see_bank_routing_scheme": false,
            "can_see_bank_routing_address": false,
            "can_see_bank_account_routing_scheme": false,
            "can_see_bank_account_routing_address": false,
            "can_see_other_bank_routing_scheme": false,
            "can_see_other_bank_routing_address": false,
            "can_see_other_account_routing_scheme": false,
            "can_see_other_account_routing_address": false
        }
    ],
    "account_routing": [
        {
            "scheme": "IBAN",
            "address": "GR0901109720000097226400154"
        },
        {
            "scheme": "AccountNumber",
            "address": "97226400154"
        }
    ]
}
```


Created by **NBG**. 
See more at https://developer.nbg.gr/

