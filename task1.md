
# GTM Event Schema

| Event Name                | Trigger Type             | Key Parameters                               | GA4 Report / Audience    |
|---------------------------|--------------------------|----------------------------------------------|--------------------------|
| page_view                 | Page View                | page_name, page_url, page_title              | Pages and Screens Report |
| clinic_page_view          | Page View                | clinic_name, city, page_url                  | Pages and Screens Report |
| booking_step_complete     | Custom Event (dataLayer) | clinic_location, specialty, step_number      | Funnel Exploration       |
| booking_completed         | Custom Event (dataLayer) | booking_id, clinic_location, specialty       | Conversions Report       |
| call_button_click         | Click                    | page_name, button_location, clinic_name      | Events Report            |
| whatsapp_click            | Click                    | page_name, clinic_name, whatsapp_link        | Events Report            |
| patient_guide_form_submit | Form Submit              | phone_provided, guide_name, page_name        | Lead Generation Report   | 
| patient_guide_download    | File Download            | file_name, file_type, page_name              | Events Report            |
| blog_scroll               | Scroll Depth             | page_title, scroll_percent, article_category | Engagement Report        |
| blog_read_complete        | Scroll Depth (90%)       | page_title, scroll_percent, article_category | Engagement Report        |



# Booking Funnel Tracking

The appointment booking form has three steps. Each step pushes a booking_step_complete event with a different step_number value.
This helps identify where users leave the booking process.

# Step 1 – Select Clinic and Specialty

{
  "event": "booking_step_complete",
  "step_number": 1,
  "step_name": "location_specialty_selected",
  "clinic_location": "Bengaluru",
  "specialty": "Orthopaedics"
}

# Step 2 – Enter Patient Details


{
  "event": "booking_step_complete",
  "step_number": 2,
  "step_name": "patient_details_entered",
  "phone_provided": true,
  "preferred_date": "2026-07-05"
}


## Step 3 – Confirm Booking

{
  "event": "booking_step_complete",
  "step_number": 3,
  "step_name": "booking_confirmed",
  "clinic_location": "Bengaluru",
  "booking_status": "Confirmed"
}


## Booking Completed

{
  "event": "booking_completed",
  "booking_id": "BK1001",
  "clinic_location": "Bengaluru",
  "specialty": "Orthopaedics"
}


# GTM Trigger for Each Step

 Booking Step      | GTM Trigger 
-------------------------------------------------------------------
 Step 1            | Custom Event Trigger ('booking_step_complete') 
 Step 2            | Custom Event Trigger ('booking_step_complete') 
 Step 3            | Custom Event Trigger ('booking_step_complete') 
 Booking Completed | Custom Event Trigger ('booking_completed') 


# Funnel Tracking in GA4

I will create a Funnel Exploration report in GA4 using the following events:

Step 1:
event = booking_step_complete
step_number = 1

Step 2:
event = booking_step_complete
step_number = 2

Step 3:
event = booking_step_complete
step_number = 3

Final Step :
event = booking_completed

This will help us understand where users leave the booking process. If many users leave after Step 2, we can improve that part of the booking form.


# Google Ads Conversion

Conversion Event:  'booking_completed'

# Reason :

I will import the booking_completed event into Google Ads because it represents a successful consultation booking. This is the main business goal of the landing page. Other events like Call Button Click or WhatsApp Click show user interest, but they do not always result in an actual appointment. Using the final booking event allows Google Ads to optimize campaigns for real conversions instead of only measuring engagement.
