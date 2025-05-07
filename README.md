# 🚀 RCS Unlocked: Send Rich Messages in 60 Minutes

Welcome to this 60-minute hands-on lab for intermediate Twilio users at [SIGNAL 2025](https://signal.twilio.com/2025)!

---

## 📚 Table of Contents

1. [Workshop Overview](#workshop-overview)
2. [Workshop Objectives](#workshop-objectives)
3. [Prerequisites](#prerequisites)
4. [Rich Messaging Concepts](#rich-messaging-concepts)
5. [Twilio Console UI Experience](#twilio-console-ui-experience)
6. [Resources](#resources)
7. [Getting Started](#getting-started)
    - [Step 1: Create a Promotional Message Template (Choose One)](#step-1-create-a-promotional-message-template-choose-one)
    - [Step 2: Present Package or A La Carte Menu](#step-2-present-package-or-a-la-carte-menu)
    - [Step 3: Show Package Options as a Carousel](#step-3-show-package-options-as-a-carousel)
    - [Step 4: Request Delivery Location](#step-4-request-delivery-location)
    - [Step 5: Send Order Summary with Action Chips](#step-5-send-order-summary-with-action-chips)
    - [Step 6: Confirm Payment Using Stored Method](#step-6-confirm-payment-using-stored-method)
    - [Step 7: Send Order Confirmation](#step-7-send-order-confirmation)
    - [Step 8: Send Transactional Update with Quick Action and Call Option](#step-8-send-transactional-update-with-quick-action-and-call-option)

---

## Workshop Overview

RCS (Rich Communication Services) is the next big thing in messaging and it's already making waves. Twilio already delivers over 750M RCS messages every month! 

In this lab, you'll learn how to:
- Set up and onboard for RCS messaging with Twilio
- Send rich, branded messages using a Messaging Service
- Build and test RCS messages in real-time

Come see how Twilio + RCS can help you create powerful, interactive messaging experiences for your users.

---

## Workshop Objectives

- [ ] Create an RCS Sender and whitelist RCS-enabled test phone number
- [ ] Add the RCS Sender to a Messaging Service
- [ ] Send Rich Messages using a Messaging Service

---

## Prerequisites

Before the workshop, make sure to have the following:

1. **RCS Access Approved**

Your Twilio account must be approved for RCS *before* the workshop. Request access using [this form](https://www.twilio.com/en-us/messaging/channels/rcs#request-access-form)

*If you didn't fill this out ahead of time and still need access during the session, you can use [this expedited access form](https://docs.google.com/forms/d/e/1FAIpQLScj6ZFA1R-r712nU8l0YygFYCVlf0Fg_3mtuc-5r9RPkAs8mw/viewform) to request access*

2. **An SMS-capable Twilio Phone Number**

This number must be registered/verified and belong to your RCS-enabled Twilio account.

3. **A Basic Understanding of Twilio Messaging**

You should be familiar with:

* [Message Resource](https://www.twilio.com/docs/messaging/api/message-resource)
* [Messaging Services](https://www.twilio.com/docs/messaging/services)

4. **An RCS-enabled Mobile Device**

---

## Rich Messaging Concepts

### Basic Terminology

- **Content Sid**  
  A unique identifier for a content template. It is a 34-character string that starts with `HX`, and can only be used by the Twilio Account SID that created it.

- **Content Variables**  
  Placeholders used to substitute values at runtime in a content template. When creating a template with variables, sample values are typically required.

- **Content Types**  
  Twilio’s omnichannel representation of rich content. Many types can be used interchangeably across messaging channels with no customization. However, some components within a content type may be incompatible with certain channels, even if the type is generally supported.

- More information about our Rich Content system can be found here: [Content Docs](https://www.twilio.com/docs/content)

---

### Twilio Console UI Experience

Twilio offers a visual interface for managing your rich messaging content. From the [Console](https://console.twilio.com/), you can:

- Create and manage content templates
- Add variables and see real-time previews
- Associate templates with Messaging Services

📸 **Example Screenshot**  
![Content Template UI](./assets/content-template-ui.png)  

🔗 [Learn more in the Twilio Docs](https://www.twilio.com/docs/content/create-templates-with-the-content-template-builder)

---

## Resources

### 🧑‍💻 Postman Collection

[Download Signal RCS Rich Messaging.postman_collection.json](./assets/Signal-RCS-Rich-Messaging.postman_collection.json)  

---

## Getting Started

### Step 1: Create a Promotional Message Template (Choose One)

Start by creating a rich promotional message template. You can choose either a carousel (multiple cards) or a single rich card with media. You can do this with no code in the UI or with the snippets below. For this demo we'll use the code snippets. 

#### Option A: Create a Carousel Template (Multiple Cards)

This option creates a [carousel template](https://www.twilio.com/docs/content/carousel) with multiple event cards and actions.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "3 events more",
   "language": "en",
   "variables": {
       "1": "Amy"
   },
   "types": {
       "twilio/carousel": {
                "body": "Hi, {{1}} 👋 \nTotal Tailgate here to share upcoming events in your preferred area!",
                "cards": [
                    {
     "title":"Hootie & the Blowfish",
     "body":"September 26, 2024",
     "media":"https://sepia-heron-4404.twil.io/assets/HootieAndTheBlowfish.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"For sure!",
         "id":"for_sure"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://www.livenation.com/artist/K8vZ9171oJV/hootie-the-blowfish-events?awtrc=true&c=SEM_LNConcertautomation_ggl_21359047336_166213539074_hootie%20%26%20the%20blowfish%20tour&GCID=0&&gad_source=1&gclid=Cj0KCQjwrp-3BhDgARIsAEWJ6SxQzE1OIBg-JoJUilCNSSo0d4CuQpwnJ9O-Pm8dzUmkoCgc6gkqJ2EaAjeZEALw_wcB&gclsrc=aw.ds"
       }
     ]
   },
   {
     "title":"Eagles vs TB Bucs",
     "body":"September 29, 2024",
     "media":"https://sepia-heron-4404.twil.io/assets/Bucs%20vs%20Eagles.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"Count me in!",
         "id":"im_in"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://www.ticketmaster.com/tampa-bay-buccaneers-tickets/artist/806026"
       }
     ]
   },
   {
     "title":"Hurricanes vs TB Bolts!",
     "body":"September 27, 2024",
     "media":"https://sepia-heron-4404.twil.io/assets/Bolts%20vs%20Hurricanes.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"Heck, yeah!",
         "id":"heck_yeah"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://tickets-center.com/tickets/v/Amalie-Arena/9618/e/NHL-Preseason/5052828/?eventId=5052828&eventName=NHL+Preseason%3a+Nashville+Predators+at+Tampa+Bay+Lightning&venueName=Amalie+Arena&venueId=9618&eventDateTime=09%2f27%2f2024+19%3a00%3a00&city=Tampa&stateProvince=FL&performerId=841&performerName=Tampa+Bay+Lightning&cid=645192248057&nid=1&accid=4186221823&campaignid=1532181056&adgroupid=65059184092&wsvar=1-645192248057+%5bgclid%7cCj0KCQjwrp-3BhDgARIsAEWJ6SwYKFAqALmnyzMDJFYZUJJmsS6BLsjhd533vS-OVr90BcLZ-1DdEkAaAjhMEALw_wcB%5d+(ag%7c65059184092)+(uuid%7ca3a178026c274859b8886b4d3ebc9338)&gclid=Cj0KCQjwrp-3BhDgARIsAEWJ6SwYKFAqALmnyzMDJFYZUJJmsS6BLsjhd533vS-OVr90BcLZ-1DdEkAaAjhMEALw_wcB&random=4504497115793608552&device=c&ismobile=false&loc_physical_ms=200524&referer=https%3a%2f%2fwww.google.com%2f&vx=0"
       }
     ]
   },
   {
     "title":"Show Me More",
     "body":"Events",
     "media":"https://sepia-heron-4404.twil.io/assets/more%20events.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"Show Me More in Tampa",
         "id":"show_me_more_my_pref_loc"
       },
       {
           "type":"URL",
           "title":"Show More in Another Area",
           "url":"https://twilio.com/"
       }
     ]
   }
]
       }
   }
}'
```
</details>

Output: `Content SID: HX4c3e08a18d3f05b564a226badf638cf7`

Next, send the carousel message to a user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX4c3e08a18d3f05b564a226badf638cf7" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

#### Option B: Create a Rich Card Template with Media

This option creates a single [rich card](https://www.twilio.com/docs/content/twiliocard) with media, quick actions, and links.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "media with chiplist w 2 urls and 1 phone number",
   "language": "en",
   "variables": {
       "1": "Amy"
   },
   "types": {
       "twilio/card": {
           "title": "Hi {{1}}! 👋 \nTotal Tailgate, here!",
           "media": ["https://sepia-heron-4404.twil.io/assets/Total%20Tailgate.png"],
           "subtitle": "To unsubscribe, reply Stop",
           "actions": [
               {"url": "https://www.hootie.com/", "title": "HOOTIE!", "type": "URL"},
               {"url": "https://www.nhl.com/lightning/", "title": "Bolts vs. Hurricanes", "type": "URL"},
               {"phone": "+17277328175", "title": "Call Total Tailgate", "type": "PHONE_NUMBER"}
           ]
       },
       "twilio/text": {
           "body": "Hi {{1}}! Total Tailgate, here! Reply EVENTS to get a list of upcoming events in your area!"
       }
   }
}'
```
</details>

Output: `Content SID: HXaa7686847b4a35ced2c080d5a841b37a`

Next, send the rich card message to a user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HXaa7686847b4a35ced2c080d5a841b37a" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

---

### Step 2: Present Package or A La Carte Menu

Create a template that prompts the user to choose between a package or an a la carte menu using quick replies.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "pkg or a la carte",
   "language": "en",
   "variables": {"1":"Amy"},
   "types": {
       "twilio/card": {
                   "title": "Super choice, {{1}}! Do you want a Package or choose from our A la Carte Menu?",
                   "actions": [
                       {
                           "title": "Package",
                           "type": "QUICK_REPLY",
                           "id": "package"
                       },
                       {
                           "title": "A la Carte Menu",
                           "type": "QUICK_REPLY",
                           "id": "alacarte"
                       }
                   ]
               },
       "twilio/text": {
           "body": "Super choice, {{1}}! Do you want a Package or choose from our A la Carte Menu?"
       }
   }
}'
```
</details>

Output: `Content SID: HX4f5dd3d8824daa877df42546f2fdd6a9`

Next, send the package or a la carte menu to the user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX4f5dd3d8824daa877df42546f2fdd6a9" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

---

### Step 3: Show Package Options as a Carousel

Create a carousel template that displays available package options, each with actions.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "packages",
   "language": "en",
   "variables": {
       "1": "Twilio"
   },
   "types": {
       "twilio/carousel": {
                "body": "Choose a Package",
                "cards": [
                    {
     "title":"The Whole Sha-bang!",
     "body":"Party for 20 with BBQ",
     "media":"https://sepia-heron-4404.twil.io/assets/thewholeshabang.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"For sure!",
         "id":"for_sure"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://sepia-heron-4404.twil.io/assets/thewholeshabang_desc.png"
       }
     ]
   },
   {
     "title":"Game on!",
     "body":"Party for 10 with BBQ",
     "media":"https://sepia-heron-4404.twil.io/assets/gameon.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"Count me in!",
         "id":"im_in"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://sepia-heron-4404.twil.io/assets/gameon_desc.png"
       }
     ]
   },
   {
     "title":"All in!",
     "body":"Party for 20",
     "media":"https://sepia-heron-4404.twil.io/assets/allin.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"Heck, yeah!",
         "id":"heck_yeah"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://sepia-heron-4404.twil.io/assets/allin_desc.png"
       }
     ]
   },
   {
     "title":"Party on!",
     "body":"Party for 10",
     "media":"https://sepia-heron-4404.twil.io/assets/partyon.png",
     "actions":[
       {
         "type":"QUICK_REPLY",
         "title":"Ready to Party!",
         "id":"ready_to_party"
       },
       {
         "type":"URL",
         "title":"See more info",
         "url":"https://sepia-heron-4404.twil.io/assets/partyon_desc.png"
       }
     ]
   }
]
       }
   }
}'
```
</details>

Output: `Content SID: HX12da7e1c56ac98c8739d8090fc4fb602`

Next, send the package options carousel to the user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX12da7e1c56ac98c8739d8090fc4fb602" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

---

### Step 4: Request Delivery Location

Prompt the user to reply with their delivery location using a simple RCS text message.

---

### Step 5: Send Order Summary with Action Chips

Create a template that summarizes the order and provides quick reply chips for confirmation, editing, or calling support.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "order summary card Chip list w 2 quick replies and 1 phone number",
   "language": "en",
   "variables": { "1": "Amy"},
   "types": {
       "twilio/card": {
                   "title": "Thank you, {{1}}. Please review your Total Tailgate Order Summary below and Confirm or Edit. \n   Order Summary \n   . \n   . \n   . \n   . ",
                   "subtitle": "To unsubscribe, reply Stop",
                   "actions": [
                       {
                           "id": "confirm",
                           "title": "CONFIRM",
                           "type": "QUICK_REPLY"
                       },
                       {
                           "id": "edit",
                           "title": "EDIT",
                           "type": "QUICK_REPLY"
                       },
                       {
                           "phone": "+17277328175",
                           "title": "Call Total Tailgate",
                           "type": "PHONE_NUMBER"
                       }
                   ]
               },
       "twilio/text": {
           "body": "Please review your Total Tailgate Order Summary. REPLY either CONFIRM or EDIT"
       }
   }
}'
```
</details>

Output: `Content SID: HX921836a9f710b0ba613d522218cd0724`

Next, send the order summary with action chips to the user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX921836a9f710b0ba613d522218cd0724" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

---

### Step 6: Confirm Payment Using Stored Method

Create a payment confirmation template that allows the user to confirm or pause payment, and provides a call option.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "payment confirmation chip list w 2 quick replies and 1 phone number",
   "language": "en",
   "variables": { "1": "Amy"},
   "types": {
       "twilio/card": {
                   "title": "{{1}}, to complete your order, Total Tailgate will bill your stored payment method. Please Confirm Payment or Pause Order. If you Pause Order, please call Total Tailgate to use a different payment method.",
                   "media": ["https://sepia-heron-4404.twil.io/assets/Total%20Tailgate.png"],
                   "subtitle": "To unsubscribe, reply Stop",
                   "actions": [
                       {
                           "id": "confirm_payment",
                           "title": "CONFIRM PAYMENT",
                           "type": "QUICK_REPLY"
                       },
                       {
                           "id": "pause_order",
                           "title": "PAUSE ORDER",
                           "type": "QUICK_REPLY"
                       },
                       {
                           "phone": "+17277328175",
                           "title": "Call Total Tailgate",
                           "type": "PHONE_NUMBER"
                       }
                   ]
               },
       "twilio/media": {
                   "body": "{{1}}, to complete your order, Total Tailgate will bill your stored payment method. Please  REPLY PAY or PAUSE. If you PAUSE, please call Total Tailgate to use a different payment method.",  
                   "media": ["https://sepia-heron-4404.twil.io/assets/Total%20Tailgate.png"]
                   }


   }
}'
```
</details>

Output: `Content SID: HX9a32a4307bc4e420c521f75e7eceeaf8`

Next, send the payment confirmation message to the user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX9a32a4307bc4e420c521f75e7eceeaf8" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

---

### Step 7: Send Order Confirmation

You have multiple options for confirming the order:

**Option 1: Send PNG Receipt with Message Body**

Create and send a media template with a PNG receipt and confirmation message.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "order confirmation png",
   "language": "en",
   "variables": {"1":"Amy"},
       "types": {
       "twilio/media": {
       "body": "👋 Hi {{1}}, Total Tailgate, here! Thank you for your order.",    
       "media": ["https://sepia-heron-4404.twil.io/assets/TT%20order%20receipt.png"]
       }
   }
}'
```
</details>

Output: `Content SID: HX6bca18ddf61bb5b7e554d873fbf4fc51`

Next, send the order confirmation RCS with media PNG and body.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX6bca18ddf61bb5b7e554d873fbf4fc51" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

**Option 2: Send PDF Receipt (No Message Body)**

Create and send a media template with a PDF receipt (no message body allowed).

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "order confirmation pdf",
   "language": "en",
       "types": {
       "twilio/media": {        
       "media": ["https://sepia-heron-4404.twil.io/assets/TT%20order%20receipt.pdf"]
       }
   }
}'
```
</details>

Output: `Content SID: HXda90b029a8c48dacbfdfd0152c054df5`

Next, send the order confirmation RCS with media PDF and no body.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HXda90b029a8c48dacbfdfd0152c054df5" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

**Option 3: Send PDF on Rich Card (May Fail with Error)**

Create and send a rich card template with a PDF, message body, and call-to-action. (Note: This may fail with a 63021 invalid content error.)

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "pdf w body and 1 phone number",
   "language": "en",
   "variables": { "1": "Amy"},
   "types": {
       "twilio/card": {
                   "title": "{{1}}, attached is your Total Tailgate Order Confirmation. Please call Total Tailgate or ASSISTANCE if further assistance is needed.",
                   "media": ["https://sepia-heron-4404.twil.io/assets/TT%20order%20receipt.pdf"],
                   "subtitle": "To unsubscribe, reply Stop",
                   "actions": [
                       {
                           "id": "assistance",
                           "title": "ASSISTANCE",
                           "type": "QUICK_REPLY"
                       },
                       {
                           "phone": "+17277328175",
                           "title": "Call Total Tailgate",
                           "type": "PHONE_NUMBER"
                       }
                   ]
               },
       "twilio/media": {
                   "body": "{{1}}, here is your Total Tailgate Order Confirmation. Please call Total Tailgate or Reply ASSISTANCE if further assistance is needed.",  
                   "media": ["https://sepia-heron-4404.twil.io/assets/TT%20order%20receipt.png"]
                   }


   }
}'
```
</details>

Output: `Content SID: HX8c4dc565a972de9f14bb12cf63492945`

Next, send the order confirmation rich card template (PDF and body and 1 action).

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX8c4dc565a972de9f14bb12cf63492945" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>

---

### Step 8: Send Transactional Update with Quick Action and Call Option

Create a rich card template for transactional updates, including a quick reply for assistance and a call button for the coordinator.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST 'https://content.twilio.com/v1/Content' \
-H 'Content-Type: application/json' \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN \
-d '{
   "friendly_name": "tranactional update with options for assistance",
   "language": "en",
   "variables": { "1": "Amy", "2": "12:00 PM", "3": "September 26", "4": "Lot 5 Raymond James Stadium"},
   "types": {
       "twilio/card": {
                   "title": "Hello {{1}}, your delivery is expected at {{2}} on {{3}} at {{4}}. Please call Total Tailgate or ASSISTANCE if further assistance is needed.",
                   "media": ["https://sepia-heron-4404.twil.io/assets/Total%20Tailgate.png"],
                   "subtitle": "To unsubscribe, reply Stop",
                   "actions": [
                       {
                           "id": "assistance",
                           "title": "ASSISTANCE",
                           "type": "QUICK_REPLY"
                       },
                       {
                           "phone": "+17277328175",
                           "title": "Call Total Tailgate",
                           "type": "PHONE_NUMBER"
                       }
                   ]
               },
       "twilio/media": {
                   "body": "Hello {{1}}, your delivery is expected at {{2}} on {{3}} at {{4}}. Please call Total Tailgate or Reply ASSISTANCE if further assistance is needed.",  
                   "media": ["https://sepia-heron-4404.twil.io/assets/Total%20Tailgate.png"]
                   }


   }
}'
```
</details>

Output: `Content SID: HX61dce72ab43b9867fbf61018c9a64f69`

Next, send the transactional update message to the user.

<details>
  <summary>Click to view the code</summary>

```
curl -X POST https://api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/Messages.json \
--data-urlencode "From=MGf4a7e201d54c623e6e3f1a91e5a17630" \
--data-urlencode "To=+18138958197" \
--data-urlencode "ContentSid=HX61dce72ab43b9867fbf61018c9a64f69" \
-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN | json_pp
```
</details>
