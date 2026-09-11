# PDM-internal_feedback_form

Internal iO-branded feedback form wired to an n8n production webhook.

- Webhook (production): https://workflows.iobonzai.com/webhook/pdm-feedback-intake
- Method: POST (JSON)
- Authentication: None (MVP) — to be locked down later via allowed origins + auth

## GitHub Pages

This repository serves the form from the `/docs` folder.

Steps to enable Pages:
1. Go to Settings → Pages
2. Source: "Deploy from a branch"
3. Branch: `main`, Folder: `/docs`
4. Save

The site will be available at:
- https://bolans1.github.io/PDM-internal_feedback_form/

Robots are blocked (`docs/robots.txt`) and the page has `<meta name="robots" content="noindex, nofollow">`.

## n8n CORS / Allowed Origins

For MVP, Allowed Origins can remain `*`. After Pages is live, restrict to:
- `https://bolans1.github.io`

## JSON payload

The form sends a JSON body matching displayed fields, plus a `_meta` object:

```json
{
  "gever_rol": "Delivery Manager|Project Manager|Peer|Domain Lead",
  "coachee_naam": "...",
  "gever_naam": "...",
  "datum_feedback": "YYYY-MM-DD",
  "Expectations": "...",
  "Core Values": "...",
  "Competence": "...",
  "Performance": "...",
  "Potential": "...",
  "overall_score": "...",
  "feedback_gedeeld_met_coachee": "true|false",
  "_meta": {
    "form_variant": "internal",
    "page_url": "...",
    "user_agent": "..."
  }
}
```

## Next steps
- After E2E verification, tighten Allowed Origins and add downstream SharePoint write + LLM extraction in n8n.
