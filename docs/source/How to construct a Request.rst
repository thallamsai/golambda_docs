How to construct a Request
====================================

Sample Request Format
^^^^^^^^^^^^^^^^^^^^^

.. jsonschema::

{
  "subIntent": "default",
  "intent": "greetings",
  "context": {
    "domain": "GI",
    "last_name": "Shenoy",
    "user_key": "+917899057774",
    "user_type": 0,
    "analytics": {
      "sub_vertical": "DF"
    },
    "from": "bharath.shenoy@goibibo.com",
    "intent": "greetings",
    "contextIntent": {
      "score": 0.0,
      "intent": "offers.list"
    },
    "conversation_id": "000fb1a6-17ad-4bc2-900a-181a67940f51",
    "message": "Earn gocash+ by confirming my check-in",
    "trip_id": "GI_WHATSAPP_+917899057774",
    "e": {
      "locale": "en",
      "intent": "goMundu.customer.checkin"
    },
    "first_name": "Bharath",
    "user_id": 27454860,
    "success": true,
    "_user_id": "9a106c22-ce8c-425a-a07a-fd0a2d234872",
    "mobile": "+917899057774",
    "email": "bharath.shenoy@goibibo.com",
    "channel": "Whatsapp",
    "gi_trace_id": "f5597600-6b87-426c-b47a-0f7c8ab05692",

    "inhouse_entities": {
      "is_international": false,
      "childs": 0,
      "adults": 0,
      "subIntent": "",
      "locale": "en",
      "stars": 0
    },


    "golambda_context": { 
    }

  }
}

Above is a sample request require to hit Golambda ActionHandler API. At root level it contains the following three keys:

Intent
***********

This is the alias of the intent you want to call.

SubIntent
***********

A particular intent can have more than one action associated with it. `subIntent` is the alias of the Action class.

Context
***********

This is a map of entities which defines the requirement of an intent. Intent uses these keys to take any actions.


User Information
********************

1. domain
2. last_name/ first_name
3. user_id
4. mobile
5. email
6. channel

NLP defined entities
*********************

All the entities recognised by NLP(chanakya) come under `inhouse_entities`.

1. cardinals (list of integers)
2. voyager based entities
3. Dates


GoLambda defined entities
**************************

These type of entities come into play when you asked the user a question and want some information about its current state along with the response. For e.g, if you want to store how many time you have continuously asked the same question to the user. You can store the count as some keyword `retry`, when the user responds you will get this count as

.. jsonschema::

"golambda_context":{
   "retry":5
   }

In simple words, whatever entities you defined in your flow for the saving state of the user inside `golamda_context` will come here. For more details about saving state, refer Response class.



