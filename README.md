# Kueski Flow Handoff — Setup Guide

## Deploy to GitHub Pages (one-time)

1. Push this folder as a GitHub repository.
2. In the repo → **Settings → Pages → Source**: set branch to `main`, folder to `/ (root)`.
3. Save. GitHub will give you a URL like `https://<org>.github.io/<repo>/` — share that with PMs and devs.

Every time you push, the page updates automatically (usually within 30 seconds).

---

## Adding a new flow

### 1 — Create the preview HTML
Ask Claude to build the flow. The preview file goes in:
```
flows/<FlowName>/<flow-name>-preview.html
```

### 2 — Register it in the hub
Open `index.html` and find the `const FLOWS = [` array near the top of the `<script>` block.  
Add a new object at the end of the array (before the closing comment):

```js
{
  id: 'my-new-flow',               // unique slug, no spaces
  title: 'My New Flow',
  description: 'One sentence describing what this flow does.',
  file: 'flows/MyNewFlow/my-new-flow-preview.html',
  status: 'ready',                 // 'ready' | 'wip' | 'draft'
  tags: ['onboarding'],            // free-form labels
  steps: [
    { label: 'Screen name',  desc: 'What happens here and what triggers the next state.' },
    { label: 'Another step', desc: 'Describe the state for PMs / devs.' },
  ],
  components: [
    { name: 'MyNewFlow',       path: 'packages/react/src/components/flows/MyNewFlow' },
    { name: 'MyNewSubScreen',  path: 'packages/react/src/components/flows/MyNewFlow/MyNewSubScreen' },
  ],
},
```

### 3 — Push
```bash
git add .
git commit -m "feat: add MyNewFlow handoff preview"
git push
```

Done — the flow appears in the hub instantly.

---

## File structure

```
/
├── index.html                              ← Hub (edit FLOWS array here)
├── flows/
│   ├── LoginFlow/
│   │   └── login-flow-preview.html
│   └── PersonalInfoFlow/
│       └── personal-info-flow-preview.html
└── packages/
    └── react/src/components/flows/         ← React source components
```
