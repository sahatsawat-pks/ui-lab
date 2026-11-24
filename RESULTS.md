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
- Step 4.3, failure message for the wrong title:
- Step 4.6, tool and calories in the answer of POST /api/pizza:
- Step 4.7, the line of the admin list that shows your pizza:
- Step 4.8, run 1, result, duration and pizza name:
- Step 4.8, run 2, result, duration and pizza name:
- Step 4.9 (optional), browser and result:
## Part B
1.
2.
3.
4.
5.
6.
7.