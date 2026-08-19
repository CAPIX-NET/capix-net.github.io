---
layout: page
title: Book a Demo
subtitle: See CAPIX treasury software in action
description: Request a personalised demonstration of CAPIX treasury software — CTM, CTC, CIM, Cloud Treasury and AI cashflow forecasting. We'll tailor the session to your ERP environment and treasury workflow.
image: /assets/img/CAPIX_large_logo.jpg
permalink: /demo/
---

Tell us a little about your treasury environment and we'll arrange a tailored walkthrough &mdash; usually 30 to 45 minutes over Microsoft Teams, with a CAPIX product specialist. There is no obligation, and we will not add you to any marketing list without your consent.

{%- if site.booking_url and site.booking_url != "" %}
<div class="demo-booking-banner">
  <div class="demo-booking-banner-text">
    <strong>Already know what you want to see?</strong>
    <span>Pick a time that suits you and book the demo directly.</span>
  </div>
  <a href="{{ site.booking_url }}" target="_blank" rel="noopener" class="btn btn-primary">Book a time &rarr;</a>
</div>
{%- endif %}

<div class="demo-grid">
  <div class="demo-form-card">
    <h3>Request a demo</h3>
    {%- assign form_action = "" -%}
    {%- if site.formspree_id and site.formspree_id != "" -%}
      {%- assign form_action = "https://formspree.io/f/" | append: site.formspree_id -%}
    {%- else -%}
      {%- assign form_action = "mailto:info@capix.net?subject=Demo%20request" -%}
    {%- endif -%}
    <form class="demo-form" action="{{ form_action }}" method="POST">
      <div class="form-row">
        <label for="demo-name">Your name <span class="req">*</span></label>
        <input id="demo-name" name="name" type="text" required autocomplete="name">
      </div>
      <div class="form-row">
        <label for="demo-email">Work email <span class="req">*</span></label>
        <input id="demo-email" name="email" type="email" required autocomplete="email">
      </div>
      <div class="form-row form-row-split">
        <div>
          <label for="demo-company">Company <span class="req">*</span></label>
          <input id="demo-company" name="company" type="text" required autocomplete="organization">
        </div>
        <div>
          <label for="demo-role">Role / title</label>
          <input id="demo-role" name="role" type="text" autocomplete="organization-title">
        </div>
      </div>
      <div class="form-row form-row-split">
        <div>
          <label for="demo-country">Country</label>
          <input id="demo-country" name="country" type="text" autocomplete="country-name">
        </div>
        <div>
          <label for="demo-phone">Phone (optional)</label>
          <input id="demo-phone" name="phone" type="tel" autocomplete="tel">
        </div>
      </div>
      <div class="form-row">
        <label for="demo-product">Which product are you interested in?</label>
        <select id="demo-product" name="product">
          <option value="">No preference / not sure yet</option>
          <option value="CTM">CAPIX Treasury Manager (CTM)</option>
          <option value="CTC">CAPIX Treasury Centre (CTC)</option>
          <option value="CIM">CAPIX Investment Manager (CIM)</option>
          <option value="CCT">Cloud Treasury (CCT)</option>
          <option value="AI">AI for Treasury</option>
          <option value="ERP">ERP Integration (Dynamics 365 / SAP)</option>
        </select>
      </div>
      <div class="form-row">
        <label for="demo-erp">Current ERP / treasury system (optional)</label>
        <input id="demo-erp" name="erp" type="text" placeholder="e.g. Dynamics 365 F&amp;O, SAP S/4HANA, FinanceOne, none">
      </div>
      <div class="form-row">
        <label for="demo-message">What would you like to see in the demo?</label>
        <textarea id="demo-message" name="message" rows="4" placeholder="Cashflow forecasting, hedge accounting, multi-entity consolidation, AI agent capabilities&hellip;"></textarea>
      </div>
      <!-- Honeypot field for spam bots; humans should leave this blank -->
      <div class="form-row form-row-honeypot" aria-hidden="true">
        <label for="demo-website">Website (leave blank)</label>
        <input id="demo-website" name="_gotcha" type="text" tabindex="-1" autocomplete="off">
      </div>
      <div class="form-actions">
        <button type="submit" class="btn btn-primary">Send request</button>
        <span class="form-note">We typically reply within one business day (AEST).</span>
      </div>
    </form>
  </div>

  <aside class="demo-side-card">
    <h3>Prefer to talk?</h3>
    <p>If you'd rather skip the form, you can reach us directly:</p>
    <ul class="demo-direct-list">
      <li><strong>Phone (Aus):</strong> <a href="tel:+611300650055">1300 65 0055</a></li>
      <li><strong>Phone (Int'l):</strong> <a href="tel:+61395212888">+613 9521 2888</a></li>
      <li><strong>Email:</strong> <a href="mailto:info@capix.net?subject=Demo%20request">info@capix.net</a></li>
    </ul>
    {%- if site.booking_url and site.booking_url != "" %}
    <p style="margin-top:1.25rem;"><a href="{{ site.booking_url }}" target="_blank" rel="noopener" class="btn btn-secondary">Book a time directly &rarr;</a></p>
    {%- endif %}
    <hr>
    <h4>What to expect</h4>
    <ul class="demo-expect-list">
      <li>30&ndash;45 minute walkthrough over Microsoft Teams</li>
      <li>Tailored to your ERP and treasury workflow</li>
      <li>Live Q&amp;A with a CAPIX product specialist</li>
      <li>No sales pressure &mdash; technical-first</li>
    </ul>
  </aside>
</div>

<p style="font-size:0.85rem;color:#6b7280;margin-top:1.5rem;">
By submitting this form you consent to CAPIX contacting you in relation to your enquiry. We handle your information in accordance with our <a href="/privacy/">Privacy Policy</a>.
</p>
