 # ⚠️ Deprecated — Legacy Routers

> **These files are not used by the running application.**
> All routes have been consolidated into [`../main.py`](../main.py).

---

## What Is This Directory?

These are standalone Flask prototypes built during early development. They have since been superseded by the unified route definitions in `main.py` and are kept here for reference only.

---

## File Status

| File                            | Status        | Notes                                           |
|---------------------------------|---------------|-------------------------------------------------|
| `dashboard.py`                  | ❌ Unused     | Duplicated in `main.py`                         |
| `risk.py`                       | ❌ Unused     | Duplicated in `main.py`                         |
| `roads.py`                      | ❌ Unused     | Older prototype with simpler detection logic    |
| `sos.py`                        | ❌ Unused     | CLI-only class — not a Flask app                |
| `reports_localized_example.py`  | 📝 Example    | Blueprint example, never registered             |

---

## What Should I Do With This?

**To clean up (recommended):**
Delete this directory — `main.py` already contains all active routes.

```bash
rm -rf legacy_routers/
```

**To integrate instead of delete:**
Register these as Flask Blueprints in `main.py` rather than running them as standalone apps.

**To extend the app with new localized routes:**
Use `reports_localized_example.py` as a starting template for adding Blueprint-based routes.

---

## Why Was This Kept?

These files serve as a reference for the original routing logic and may be useful when:
- Debugging a regression and comparing old vs. current route behaviour
- Extracting logic that wasn't fully ported to `main.py`
- Onboarding contributors who want to understand the project's evolution

