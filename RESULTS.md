# UI lab results
Tool parts that I chose:
## Part 0
- Step 0.1, Chrome version: 157.0.8103.78 (Official Build) (arm64) 
- Step 0.3, ChromeDriver version: ChromeDriver 157.0.8103.78 (4b3d0dabb8250b6f152d2d85d79e7706e309d087-refs/branch-heads/8103@{#1573})
- Step 0.4, locator of Pizza, Please!: `//button[normalize-space()='Pizza, Please!']`
- Step 0.4, locator of Excluded tools: `//label[normalize-space()='Excluded tools']/following-sibling::*[1]`
- Step 0.4, locator of Must be vegetarian: `//label[normalize-space()='Must be vegetarian']/preceding-sibling::input[@type='checkbox']`
- Step 0.4, locator of Custom Pizza Name: `input#pizza-name`

- Step 0.5, pizza name, tool and calories of the run by hand:
| Step | Actual result | Pass or fail |
|------|---------------|--------------|
| 1 | Opened [https://quickpizza.grafana.com](https://quickpizza.grafana.com); heading displayed Looking to break out of your pizza routine? | |
| 2 | Clicked Advanced; Max Calories per Slice, Excluded tools, Must be vegetarian, and Custom Pizza Name appeared | Pass |
| 3 | Set calories to 600, selected Knife, checked Must be vegetarian, entered `Lab Pizza 20261124-222500`; fields showed those values | Pass |
| 4 | Clicked Pizza, Please!; recommendation displayed `Lab Pizza 20261124-222500`, tool `Pizza cutter`, and `500` calories per slice | Pass |
| 5 | Clicked Love it! while logged out; page showed Please log in first. | Pass |
| 6 | Opened /admin, entered admin and admin, clicked Sign in; page showed Latest pizza recommendations | Pass |
| 7 | Found Lab Pizza 20261124-222500 in the list showing (tool=`Pizza cutter`, ...) | Pass |
## Part 1: Selenium IDE
- Firefox version and Node.js version:
- Step 1.4, the line of the failed check and the line Tests: `Actual value 'Received!' did not match 'Received' during assertText:id=message:Received` | `Tests:       1 failed, 1 total`
- Step 1.5, target chosen for Submit, and why the recorded one was fragile: `xpath=//button[@type='submit']`; the recorded `css=.btn` relies on a visual/styling class that other buttons can share and matches the first `.btn` element, so adding another button above it or changing styling classes can break it, whereas `xpath=//button[@type='submit']` targets a submit button by its semantic `type` attribute.
- Step 1.6, commands changed, added or deleted after recording: Added explicit waits (`wait for element visible` / `wait for element present`), assertions (`assert text`, `assert value`, `assert selected label`, `assert checked`, `assert not text`, `assert`), `execute script` (for `pizzaName` and `<= 600` calorie check), `echo ${pizzaName}`, and `store text` (`calories`); updated targets/values to use the `Advanced` label, `Max Calories per Slice` label-to-input XPath, `add selection` `label=Knife`, `css=input#pizza-name`, `${pizzaName}`, `name=pizza-please`, and `name=rate-5`; deleted extra/redundant recorded steps and placeholder text so the test matches the 29 commands.
- Step 1.6, the pizza names of run 1 and run 2, from the lines info: echo: `Lab Pizza 20261124-234719`
- Step 1.6, the line Tests: of both runs: `Tests:       2 passed, 2 total` | Run 2: `Tests:       2 passed, 2 total`
- Step 1.7, one line of QP01customerTest.java that needs rewriting, and why: `assertThat(value, is("vars.get("pizzaName").toString()"));` — it does not compile because double quotes inside the string literal break Java syntax (and even unescaped it would compare against the literal text rather than the generated pizza name stored in `vars`).
## Part 2: Selenium WebDriver in Java
- Step 2.4, the failure line for the wrong title: [ERROR]   FirstTest.webFormOpens:18 expected: <Web Form> but was: <Web form>
- Step 2.15, QP01Test run 1, result and time: 
```
[INFO] Results:
[INFO] 
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  7.914 s
[INFO] Finished at: 2026-11-25T01:23:08+07:00
[INFO] ------------------------------------------------------------------------
```
- Step 2.15, QP01Test run 2, result and time:
```
[INFO] Results:
[INFO] 
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  7.557 s
[INFO] Finished at: 2026-11-25T01:23:40+07:00
[INFO] ------------------------------------------------------------------------
```
- Step 2.20, full run 1, time and number of tests:
```
[INFO] Results:
[INFO] 
[INFO] Tests run: 5, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.684 s
[INFO] Finished at: 2026-11-25T01:34:52+07:00
[INFO] ------------------------------------------------------------------------
```
- Step 2.20, full run 2, time and number of tests:
```
[INFO] Results:
[INFO] 
[INFO] Tests run: 5, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.926 s
[INFO] Finished at: 2026-11-25T01:35:32+07:00
[INFO] ------------------------------------------------------------------------
```
## Part 3: Robot Framework
- robot --version: Robot Framework 7.5.1 (Python 3.14.7 on darwin)
- Step 3.2, failure message for the wrong title: 
```
FAIL |
Title should have been 'Web Form' but was 'Web form'.
```
- Step 3.8, run 1, result, elapsed time and pizza name:
```
Status:	All tests passed
Documentation:	
Test case QP-01, A custom pizza reaches the admin list.

Start Time:	20261125 02:48:29.689
End Time:	20261125 02:48:36.639
Elapsed Time:	00:00:06.950
```
- Step 3.8, run 2, result, elapsed time and pizza name:
```
Status:	All tests passed
Documentation:	
Test case QP-01, A custom pizza reaches the admin list.

Start Time:	20261125 02:48:39.994
End Time:	20261125 02:48:46.938
Elapsed Time:	00:00:06.944
```
## Part 4: Cypress
- node --version, npm --version and npx cypress version:
  - node --version: v26.0.0
  - npm --version: 12.2.3
  - npx cypress version: 16.2.1 (stable)
- Step 4.3, failure message for the wrong title: 
```
1) Web form
       fills in the fields and sends the form:

      Timed out retrying after 10000ms
      + expected - actual

      -'Web form'
      +'Web Form'
      
      at Context.eval (webpack://cypress/./cypress/e2e/web-form.cy.js:6:19)

```
- Step 4.6, tool and calories in the answer of POST /api/pizza:
```
tool: "Scissors"
"calories": 475
```
- Step 4.7, the line of the admin list that shows your pizza: 
```
Lab Pizza 20261125-185939 (tool=Pizza cutter, ingredients_number=5) (newest)
The Black Margherita (tool=Scissors, ingredients_number=6)
The Wise Marinara (tool=Scissors, ingredients_number=7)
The Fierce Capricciosa (tool=Scissors, ingredients_number=7)
A Fast Funghi (tool=Knife, ingredients_number=7)
An Able Capricciosa (tool=Pizza cutter, ingredients_number=5)
A Mammoth Quattro Formaggi (tool=Scissors, ingredients_number=6)
A Small Carbonara (tool=Pizza cutter, ingredients_number=5)
A Quiet Fungi e Olive (tool=Scissors, ingredients_number=8)
An Able Margherita (tool=Scissors, ingredients_number=5)
A Rough Pugliese (tool=Knife, ingredients_number=8)
An Ugly Siciliana (tool=Knife, ingredients_number=7)
A Black Frutti di Mare (tool=Scissors, ingredients_number=7)
An Orange Funghi (tool=Knife, ingredients_number=5)
The Tame Frutti di Mare (tool=Scissors, ingredients_number=6)
```
- Step 4.8, run 1, result, duration and pizza name: 
```
====================================================================

  (Run Finished)


       Spec                                              Tests  Passing  Failing  Pending  Skipped  
  ┌────────────────────────────────────────────────────────────────────────────────────────────────┐
  │ ✔  pizza-scenario.cy.js                     00:11        1  1        -        -        - │
  ├────────────────────────────────────────────────────────────────────────────────────────────────┤
  │ ✔  web-form.cy.js                           00:02        1  1        -        -        - │
  └────────────────────────────────────────────────────────────────────────────────────────────────┘
    ✔  All specs passed!                        00:14        2  2        -        -        -  

Pizza Name: Lab Pizza 20261125-190657
```
- Step 4.8, run 2, result, duration and pizza name:
```
====================================================================

  (Run Finished)


       Spec                                              Tests  Passing  Failing  Pending  Skipped  
  ┌────────────────────────────────────────────────────────────────────────────────────────────────┐
  │ ✔  pizza-scenario.cy.js                     00:07        1  1        -        -        - │
  ├────────────────────────────────────────────────────────────────────────────────────────────────┤
  │ ✔  web-form.cy.js                           00:01        1  1        -        -        - │
  └────────────────────────────────────────────────────────────────────────────────────────────────┘
    ✔  All specs passed!                        00:09        2  2        -        -        -  

Pizza Name: Lab Pizza 20261125-190850
```
- Step 4.9 (optional), browser and result:
## Part B
1. All three numeric input boxes on the QuickPizza home page share the exact same non-unique ID (`id="floating_filled"`), so `$$("#floating_filled").length` returns `3` in Chrome DevTools and cannot distinguish the calories input from the other fields. Because of that collision, the tests must traverse from the visible `<label>` text (`Max Calories per Slice`) to its sibling `<input>` element (`xpath://label[contains(.,'Max Calories')]/../input` in Robot Framework and `cy.contains('label', 'Max Calories per Slice').siblings('input')` in Cypress). Giving that input a unique, descriptive ID such as `id="max-calories-per-slice"` would allow tests to target it directly via `id:max-calories-per-slice` or `#max-calories-per-slice`. That change makes locators shorter, faster to write, and immune to breaking if the label wording or surrounding HTML layout changes.
2. Comparing the `tool` displayed on the `/admin` list entry (`(tool=...,`) against the `tool` returned on the home page recommendation in Step 4 is a **consistency oracle** (cross-checking two views/states of the same system against each other). Because the recommended tool is chosen dynamically by QuickPizza on each request, the test cannot hardcode a fixed expected string beforehand and instead verifies that both interfaces agree on the generated record. This check would catch a backend persistence or mapping bug where the `/api/pizza` endpoint returns one tool (such as `Scissors`) in the UI response, while saving a default, null, or mismatched tool value in the database shown on `/admin`.
3. To verify that the generated pizza actually satisfies the `Must be vegetarian` restriction, the test can inspect the ingredients returned in the `POST /api/pizza` network response or displayed on the recommendation card and assert that none belong to a known list of non-vegetarian items (or check the response payload's `"vegetarian": true` field alongside its `ingredients` array). In Cypress, `cy.intercept('POST', '/api/pizza').as('pizza')` already captures `response.body`, so the test could assert `expect(response.body.vegetarian).to.be.true` and verify `response.body.pizza.ingredients` against a list of meat toppings. For a purely UI-based check in Robot Framework, the page would need to render either a visible vegetarian badge/status in `#recommendations` or list every ingredient name with clear dietary metadata so the test can validate them against an allowed vegetarian ingredient list.
4. Robot Framework required explicit `Wait Until ...` keywords (such as `Wait Until Element Is Visible css:h1` and `Wait Until Page Contains Element id:svelte-announcer`) paired with `timeout=10s`, whereas Cypress automatically retried every `cy.get()` and `.should()` assertion up to `defaultCommandTimeout: 10000` without manual wait steps—and even let us assert directly on `POST /api/pizza` via `cy.intercept`. Writing QP-01 was noticeably faster in Cypress because chaining commands and inspecting `request.body`/`response.body` required less boilerplate than maintaining separate `.robot` and `.resource` keyword definitions and importing `String` and `DateTime` libraries. For debugging and evidence, both tools produced clear artifacts: Robot Framework generated detailed step-by-step `log.html` reports with embedded screenshots (`qp01-step3-fields.png` through `qp01-step7-admin-list.png`), while Cypress recorded a full `.mp4` video (`pizza-scenario.cy.js.mp4`) showing the Command Log synchronized side-by-side with the browser view.
5. For Project 2, I would choose **Cypress** as the automated UI testing tool. First, Cypress's built-in automatic retrying (`defaultCommandTimeout`) and native network interception (`cy.intercept` and `cy.wait('@alias')`) eliminate flaky timing issues on dynamic pages while verifying both the UI and backend API payloads in one flow. Second, Cypress's interactive runner, automatic failure screenshots, and full-run `.mp4` video recordings (`video: true`) provide immediate visual debugging and ready-to-submit test evidence without needing external screen-recording software or manual ChromeDriver version matching.
6. If QuickPizza changed the locator of the `Max Calories per Slice` input box, you would only update the `${MAX CALORIES}` variable in one place inside `robot/resources/quickpizza.resource` (under `*** Variables ***`). Because both `Turn On Advanced` (which checks `Element Should Be Visible ${MAX CALORIES}`) and `Fill In The Pizza Request` (which runs `Input Text ${MAX CALORIES}` and `Textfield Value Should Be ${MAX CALORIES}`) reference that single variable, `pizza_scenario.robot` never contains raw XPath or CSS selectors. Keeping all locators isolated in the resource file prevents cascading edits across test cases whenever the application's DOM changes.
7. Cypress automatically clears browser cookies and local storage before every `it(...)` block to keep tests isolated. In QuickPizza, a session cookie pins the browser to the specific backend server instance that stored the pizza created in Step 4, so the `/admin` page in Steps 6–7 only displays that pizza if it runs within the same browser session. If Steps 6 and 7 were split into a second `it(...)` test, Cypress would wipe the session cookie before visiting `/admin`, potentially routing the admin request to a different QuickPizza server instance where `pizzaName` does not exist and causing `cy.contains('li', pizzaName)` to time out and fail.