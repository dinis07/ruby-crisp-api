# ruby-crisp-api

The Crisp API Ruby wrapper. Authenticate, send messages, fetch conversations, access your agent accounts from your Ruby code.

Copyright 2019 Crisp IM SARL. See LICENSE for copying information.

* **📝 Implements**: [REST API Reference (V1)](https://docs.crisp.chat/references/rest-api/v1/) at revision: 12/31/2017
* **😘 Maintainer**: [@valeriansaliou](https://github.com/valeriansaliou), [@eliottvincent](https://github.com/eliottvincent)

## Usage

You may follow the [REST API Quickstart](https://docs.crisp.chat/guides/rest-api/quickstart/) guide, which will get you running with the REST API in minutes.

Add the library to your `Gemfile`:

```bash
gem "crisp-api", "~> 1.1.6"
```

Then, import it:

```ruby
require "crisp-api"
```

Build a new authenticated Crisp client with your `identifier` and `key` tokens.

```ruby
client = Crisp::Client.new

client.set_tier("plugin")
client.authenticate(identifier, key)
```

Then, your client is ready to be consumed!

## Authentication

To authenticate against the API, obtain your authentication token keypair by following the [REST API Authentication](https://docs.crisp.chat/guides/rest-api/authentication/) guide. You'll get a token keypair made of 2 values.

**Keep your token keypair values private, and store them safely for long-term use.**

Then, add authentication parameters to your `client` instance right after you create it:

```ruby
client = Crisp::Client.new

# Authenticate to API with your plugin token (identifier, key)
# eg. client.authenticate("5c0595b2-9381-4a76-a2e0-04aa00c1ede7", "3bdb0812d0f5352bf68901ddc731434dade419b98507971905acdd2f967df61c")
client.set_tier("plugin")
client.authenticate(identifier, key)

# Now, you can use authenticated API sections.
```

## Resource Methods

Most useful available Crisp API resources are implemented. **Programmatic methods names are named after their label name in the [REST API Reference](https://docs.crisp.chat/references/rest-api/v1/)**.

Thus, it is straightforward to look for them in the library while reading the [REST API Reference](https://docs.crisp.chat/references/rest-api/v1/).

In the following method prototypes, `crisp` is to be replaced with your Crisp API instance. For example, instanciate `client = Crisp()` and then call eg: `client.website.list_conversations(website_id, 1)`.

When calling a method that writes data to the API (eg. send a message with: `client.website.send_message_in_conversation()`), you need to submit it this way:

```ruby
website_id = "6497e4a4-b17c-41e0-bfea-eea97ba8115a"
session_id = "session_f32bc993-f7ce-41af-bcd1-110fc147a392"

client.website.send_message_in_conversation(
  website_id, session_id,

  {
    "type" => "text",
    "content" => "This message was sent from python-crisp-api! :)",
    "from" => "operator",
    "origin" => "chat"
  }
)
```

### Website

* **Website Conversations**
  * **List Conversations**: `client.website.list_conversations(website_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-conversations)
  * **Search Conversations**: `client.website.search_conversations(website_id, page_number, search_query, search_type, search_operator, include_empty, filter_unread, filter_resolved, filter_not_resolved, filter_mention, filter_assigned, filter_unassigned, filter_date_start, filter_date_end, order_date_created", order_date_updated)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-conversations)

* **Website Conversation**
  * **Create A New Conversation**: `client.website.create_new_conversation(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#create-a-new-conversation)
  * **Check If Conversation Exists**: `client.website.check_conversation_exists(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#check-if-conversation-exists)
  * **Get A Conversation**: `client.website.get_conversation(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-a-conversation)
  * **Remove A Conversation**: `client.website.remove_conversation(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#remove-a-conversation)
  * **Initiate A Conversation With Existing Session**: `client.website.initiate_conversation_with_existing_session(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#initiate-a-conversation-with-existing-session)
  * **Get Messages In Conversation**: `client.website.get_messages_in_conversation(website_id, session_id, query)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-messages-in-conversation)
  * **Send A Message In Conversation**: `client.website.send_message_in_conversation(website_id, session_id, query)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#send-a-message-in-conversation)
  * **Update A Message In Conversation**: `client.website.update_message_in_conversation(website_id, session_id, fingerprint, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#update-a-message-in-conversation)
  * **Compose A Message In Conversation**: `client.website.compose_message_in_conversation(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#compose-a-message-in-conversation)
  * **Mark Messages As Read In Conversation**: `client.website.mark_messages_read_in_conversation(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#mark-messages-as-read-in-conversation)
  * **Mark Messages As Delivered In Conversation**: `client.website.mark_messages_delivered_in_conversation(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#mark-messages-as-delivered-in-conversation)
  * **Get Conversation Routing Assign**: `client.website.get_conversation_routing_assign(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-conversation-routing-assign)
  * **Assign Conversation Routing**: `client.website.assign_conversation_routing(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#assign-conversation-routing)
  * **Get Conversation Metas**: `client.website.get_conversation_metas(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-conversation-metas)
  * **Update Conversation Metas**: `client.website.update_conversation_metas(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#update-conversation-metas)
  * **List Conversation Pages**: `client.website.list_conversation_pages(website_id, session_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-conversation-pages)
  * **List Conversation Events**: `client.website.list_conversation_events(website_id, session_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-conversation-events)
  * **Get Conversation State**: `client.website.get_conversation_state(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-conversation-state)
  * **Change Conversation State**: `client.website.change_conversation_state(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#change-conversation-state)
  * **Get Block Status For Conversation**: `client.website.get_block_status_for_conversation(website_id, session_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-block-status-for-conversation)
  * **Block Incoming Messages For Conversation**: `client.website.block_incoming_messages_for_conversation(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#block-incoming-messages-for-conversation)
  * **Request Email Transcript For Conversation**: `client.website.request_email_transcript_for_conversation(website_id, session_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#request-email-transcript-for-conversation)

* **Website People**
  * **Get People Statistics**: `client.website.get_people_statistics(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-people-statistics)
  * **List People Segments**: `client.website.list_people_segments(website_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-suggested-people-segments)
  * **List People Profiles**: `client.website.list_people_profiles(website_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-people-profiles)
  * **Add New People Profile**: `client.website.add_new_people_profile(website_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#add-new-people-profile)
  * **Check If People Profile Exists**: `client.website.check_people_profile_exists(website_id, people_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#check-if-people-profile-exists)
  * **Get People Profile**: `client.website.get_people_profile(website_id, people_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-people-profile)
  * **Save People Profile**: `client.website.save_people_profile(website_id, people_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#save-people-profile)
  * **Find People Profile By Email**: `client.website.find_people_profile_by_email(website_id, email)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-people-profile)
  * **Update People Profile**: `client.website.update_people_profile(website_id, people_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#update-people-profile)
  * **Remove People Profile**: `client.website.remove_people_profile(website_id, people_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#remove-people-profile)
  * **List People Conversations**: `client.website.list_people_conversations(website_id, people_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-people-conversations)
  + **Add A People Event**: `client.website.add_people_event(website_id, people_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#add-a-people-event)
  + **List People Events**: `client.website.list_people_events(website_id, people_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-people-events)
  + **Get People Data**: `client.website.get_people_data(website_id, people_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-people-data)
  + **Save People Data**: `client.website.save_people_data(website_id, people_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#save-people-data)
  + **Update People Data**: `client.website.update_people_data(website_id, people_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#update-people-data)
  + **Get People Subscription Status**: `client.website.get_people_subscription_status(website_id, people_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-people-subscription-status)
  + **Update People Subscription Status**: `client.website.update_people_subscription_status(website_id, people_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#update-people-subscription-status)

* **Website Base**
  * **Create Website**: `client.website.create_website(data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#create-website)
  * **Get A Website**: `client.website.get_website(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-a-website)
  * **Delete A Website**: `client.website.delete_website(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#delete-a-website)

* **Website Batch**
  * **Batch Resolve Items**: `client.website.batch_resolve_items(website_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#batch-resolve-items)
  * **Batch Read Items**: `client.website.batch_read_items(website_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#batch-read-items)
  * **Batch Remove Items**: `client.website.batch_remove_items(website_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#batch-remove-items)

* **Website Availability**
  * **Get Website Availability Status**: `client.website.get_website_availability_status(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-website-availability-status)

* **Website Operator**
  * **List Website Operators**: `client.website.list_website_operators(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-website-operators)
  * **List Last Active Website Operators**: `client.website.list_last_active_website_operators(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-last-active-website-operators)

* **Website Settings**
  * **Get Website Settings**: `client.website.get_website_settings(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-website-settings)
  * **Update Website Settings**: `client.website.update_website_settings(website_id, data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#update-website-settings)

* **Website Visitors**
  * **Count Visitors**: `client.website.count_visitors(website_id)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#count-visitors)
  * **List Visitors**: `client.website.list_visitors(website_id, page_number)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#list-visitors)
  * **Get Session ID**: `client.website.get_session_id_by_token(website_id, token)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#get-session-identifier-from-token)

### Bucket

* **Bucket URL**
  * **Generate Bucket URL**: `client.bucket.generate_bucket_url(data)` [Reference](https://docs.crisp.chat/references/rest-api/v1/#generate-bucket-url)
