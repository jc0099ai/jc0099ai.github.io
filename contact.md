---
layout: page
title: Contact
permalink: /contact/
---

## Contact Me

If you would like to get in touch about research, collaboration, or other academic inquiries, please use the form below.

<form id="contact-form">

<input type="hidden"
      name="access_key"
      value="00d351a1-1d35-4ecd-8b82-70849d814082">

<input type="hidden"
      name="subject"
      value="New message">

<input type="hidden"
      name="from_name"
      value="Jess Chen's Personal Website">

<label for="name">Name</label> <input type="text"
      id="name"
      name="name"
      placeholder="Your name"
      required>

<label for="email">Email</label> <input type="email"
      id="email"
      name="email"
      placeholder="your@email.com"
      required>

<label for="message">Message</label>

  <textarea id="message"
            name="message"
            rows="8"
            placeholder="Write your message here..."
            required></textarea>

  <button type="submit" id="submit-button">
    Send Message
  </button>

  <p id="form-result"></p>

</form>

<script>
document.getElementById("contact-form").addEventListener("submit", async function(event) {

  event.preventDefault();

  const form = event.target;
  const button = document.getElementById("submit-button");
  const result = document.getElementById("form-result");

  button.disabled = true;
  button.textContent = "Sending...";
  result.textContent = "";

  const formData = new FormData(form);

  try {

    const response = await fetch(
      "https://api.web3forms.com/submit",
      {
        method: "POST",
        body: formData
      }
    );

    const data = await response.json();

    if (data.success) {

      // Clear all form fields
      form.reset();

      result.textContent = "Thank you! Your message has been sent.";

    } else {

      result.textContent =
        "Sorry, something went wrong. Please try again.";

    }

  } catch (error) {

    result.textContent =
      "Unable to send your message. Please try again later.";

  }

  button.disabled = false;
  button.textContent = "Send Message";

});
</script>
