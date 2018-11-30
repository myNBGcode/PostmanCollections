# Use case scenario
#### Welcome to the Cards Sandbox API.

------------------------------------------------------------------------------------------

### The API
This API provides a standard RESTful interface that enables a user to
* Get all the cards of the current user
* Get the cards f the current user in the specified bank


### Real life Use Case Scenario

The main functionality of the application is to aggregate financial data for the cards of a user.

First of all, we will create our sandbox by making an **HTTP POST** request to the following URL
> https://apis.nbg.gr/public/sandbox/obp.card.sandbox/oauth2/v1/sandbox

With a request body:
```json
 {
   "sandbox_id": "2F5DEDB4-F28B-40EF-B547-378299B08D36"
 }
``` 

**Note: Remember to store *sandbox_id* somewhere in your application, because you will need to provide it in as a header
in each api call.**


There exists an application, "TidyWallet", that offers the functionality of displaying information about a user's cards.
To do so, the application needs to ask the API if the user has issued a card of a specific type in a specific bank, in order to display the cards along with their details. 

The application needs to call the API multiple times for each bank and each card type, with a **HTTP GET** request to the following endpoint:
>https://apis.nbg.gr/public/sandbox/obp.card.sandbox/oauth2/v1/obp/banks/{bank_id}/cards/{card_type}

will return the results below:
<details><summary>response</summary>

```json
{
    "cards": [
        {
            "cardExtensions": null,
            "cardId": "ba44ec8b-698d-4312-b452-f95eba8f159b",
            "bank_card_number": "5278900029523359",
            "name_on_card": "sDoulfis",
            "issue_number": "52789000",
            "serial_number": "321123",
            "valid_from_date": "2018-11-29T09:12:59.433417+02:00",
            "expires_date": "2028-11-29T09:12:59.433417+02:00",
            "enabled": true,
            "cancelled": false,
            "on_hot_list": false,
            "technology": null,
            "networks": null,
            "allows": null,
            "replacement": null,
            "pin_reset": null,
            "collected": "2018-11-29T09:12:59.433417+02:00",
            "posted": "2018-11-29T09:12:59.433417+02:00",
            "account": {
                "id": "cee1db2f-39e1-4918-b3fc-2d81d3439ccc",
                "label": "SandboxNBG",
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
                    }
				...					
    ]
}
```
</details>

Created by **NBG**. 
See more at https://developer.nbg.gr/
