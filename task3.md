# Task 03 – Integration Design

## Integration Architecture

I would use the **HubSpot Forms API** to connect the landing page with HubSpot CRM because it is simple, reliable, and suitable for this project.

When a user fills in the consultation form and clicks the **Book Consultation** button, the landing page first validates the form data. If the data is valid, it sends the information to the HubSpot Forms API. The information includes the patient's name, phone number, clinic preference, source as **Google Ads – Consultation Landing Page**, and lead status as **New Enquiry**.

After HubSpot receives the data, the system should first check whether the phone number already exists in the CRM. Since HubSpot normally uses email for duplicate detection, an additional phone number lookup should be performed before creating a new contact. If the phone number already exists, the existing contact should be updated. Otherwise, a new contact should be created.

After the contact is successfully saved in HubSpot, the integration should call the **Karix WhatsApp Business API** to send a confirmation message to the patient. At the same time, the **consultation_form_submitted** conversion event should be sent to Google Ads so the campaign can optimize for successful consultation requests.

The overall flow is:

Landing Page → HubSpot Forms API → HubSpot CRM → Karix WhatsApp API → Google Ads Conversion

---

## Biggest Failure Point

The biggest failure point is the HubSpot API request. If the request fails, the patient information will not be saved in the CRM, and the following steps such as the WhatsApp confirmation and conversion tracking may also fail.

To reduce this risk, I would log failed requests and retry them automatically after a short delay. This helps prevent data loss if there is a temporary network or API issue.

---

## WhatsApp SLA Monitoring

The WhatsApp confirmation message should be delivered within two minutes after the form is submitted. This could be delayed because of internet problems, API errors, server downtime, or slow response from the WhatsApp service.

To monitor this, I would log the submission time and the message delivery status for every request. Failed or delayed messages should be recorded in an error log so they can be reviewed quickly. If a message is not sent within the expected time, the system should retry the request and notify the support team. This helps ensure that patients receive their confirmation message as soon as possible and improves the overall reliability of the system.
