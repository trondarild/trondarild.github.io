# Experiment goes here

GitHub Pages site serving the CAVAA/COGEMI survey instruments at
<https://trondarild.github.io/cavaa/>.

**This repo is a deployment target, not a place to edit.** The source of truth
for every page under `cavaa/` is `~/code/COGEMI_RL/cogemi/survey/`. Publish
with `cogemi/survey/deploy_to_pages.sh`, which checks for unfilled Prolific
completion codes, parses the inline JavaScript and runs the structural tests
before it copies, commits and pushes. Editing a file here directly means the
next deploy silently overwrites it.

## CAVAA experiment

Current study — one Prolific study, role drawn server-side at entry:

[cavaa/appropriateness_survey_aspects_park_prolific_v2_roles.html](cavaa/appropriateness_survey_aspects_park_prolific_v2_roles.html)

### Superseded

The three per-arm files (`..._v2_agent`, `..._v2_target`, `..._v2_observer`)
were replaced by the role router before their completion codes were set. They
remain deployed but no Prolific study points at them.

[cavaa/appropriateness_survey_aspects_park_prolific_v2.html](cavaa/appropriateness_survey_aspects_park_prolific_v2.html)

[cavaa/appropriateness_survey_aspects_park_prolific.html](cavaa/appropriateness_survey_aspects_park_prolific.html)

### Old

[cavaa/appropriateness_survey_aspects_ghpages.html](cavaa/appropriateness_survey_aspects_ghpages.html)

[cavaa/role_survey_ghpages.html](cavaa/role_survey_ghpages.html)

[cavaa/appropriateness_survey_ghpages.html](cavaa/appropriateness_survey_ghpages.html)

## Local testing

`cavaa/webserver.sh` and `cavaa/index.html` are scaffolding for trying a
survey out before it goes live. Both are gitignored: they are local tools, and
`index.html` would otherwise become the landing page of the published site.

```
cd cavaa && sh webserver.sh        # python3 -m http.server 8000
```

Then open <http://localhost:8000/>. `index.html` is a bare link list to
whichever survey is being worked on, with a dummy `?PROLIFIC_PID=test`
appended — the surveys check for that parameter before they will start, and
without it show the "must be accessed via your Prolific study link" page.

A locally served survey still writes to the live Supabase tables. Use a
`__smoketest__` prefix in the PID if you want the rows to be removable
afterwards with `purge_smoketest_data()`.
