# WhatsApp Business API Error: (#131037) Display Name Approval Required

![Error 131037](./images/error-131037.png)

**Last updated: January 13, 2026**

When trying to send messages through your WhatsApp Business Account (WABA), you may encounter this error message:

> **(#131037) WhatsApp provided number needs display name approval before message can be sent**

This issue occurs when your phone number's **display name has not yet been approved by Meta** (WhatsApp Business Platform). Until that approval is complete, the number cannot be used to send or receive messages through your BSP (Business Solution Provider like MEGA).

---

## 🔍 Why This Error Happens

Each WhatsApp Business phone number must have an **approved display name** before it can be activated.

When you register a new number under your WhatsApp Business Account, Meta reviews the display name to ensure it complies with WhatsApp's naming and business policies.

If your display name is still **"Under Review"** or has been **"Rejected"**, the system will block any outbound or inbound messaging, resulting in this error.

---

## ✅ How to Fix the Error

Follow these steps to resolve the issue:

### 1. Go to your Meta Business Manager

- Log in to [https://business.facebook.com/](https://business.facebook.com/)
- Open **Business Settings → Accounts → WhatsApp Accounts**

### 2. Select your WABA account and check your Phone Numbers tab

- Look for the number that shows the error
- You'll see the **Display Name Status** (e.g., "Pending Review", "Approved", or "Rejected")

### 3. If status = Pending Review

- **Wait for Meta's review to complete**
- This process typically takes up to **24–48 hours**

### 4. If status = Rejected

- Click **Edit Display Name** and resubmit it following WhatsApp's guidelines
- Avoid using generic or misleading names. It must clearly represent your business or brand
- You can refer to Meta's policy here: [WhatsApp Display Name Guidelines](https://www.facebook.com/business/help/757569725593362)

### 5. Once Approved

- The error will automatically disappear
- You'll be able to send messages normally from your BSP (like MEGA)

---

## 💡 Tip

If you've recently migrated your number to a new BSP, the display name review may restart under the new Business Manager. In that case, make sure to recheck the approval status before attempting to send messages.

---

## 🧾 Summary

| Error Code | Reason | Solution |
|------------|--------|----------|
| (#131037) WhatsApp provided number needs display name approval | The display name is pending or rejected by Meta | Check status in Business Manager → Resubmit or wait for approval |

---

## Tags

`#WhatsApp` `#Error131037` `#DisplayName` `#WABA` `#Meta` `#Troubleshooting`

---

## Related Resources

- [WhatsApp Display Name Guidelines](https://www.facebook.com/business/help/757569725593362)
- [Meta Business Manager](https://business.facebook.com/)
- [WhatsApp Business API Documentation](https://developers.facebook.com/docs/whatsapp)
- [MEGA Documentation](https://github.com/megaapp977/stack)
