# Day 2 Notes - Regression, Retesting, Smoke & Sanity Testing

*Date: 17 Oct 2026*

---

## 1. Regression Testing
Testing conducted on a **modified build** to make sure the changes (adding, deleting or modifying features) have **not affected existing functionality**.

### Types of Regression Testing

**Unit Regression Testing**
- Tests only the changes/modifications made by the developer.

**Regional Regression Testing**
- Tests the modified module along with the **impacted modules**.
- An **Impact Analysis meeting** between QA and Dev is held to identify the impacted modules.

**Full Regression**
- Tests the main feature and the remaining parts of the application.
- Example: the dev changed many modules. Instead of identifying each impacted module, QA performs one round of full regression.

### Regression Suite
A maintained set of test cases that is re-run on every build. Regression test cases are the best candidates for automation, because they are repeated every release.

---

## 2. Re-Testing (Confirmation Testing)
- Whenever the developer fixes a bug, the tester tests the bug fix. This is called **re-testing**.
- If the fix works, the tester **closes** the bug. Otherwise the tester **re-opens** it and sends it back to the developer.
- Purpose: to ensure that defects found and posted in the earlier build are fixed in the current build.
- Re-run the **same failed test case**, with the same steps and test data.

**Example:**
- Build 1.0 is released. The test team finds defects (Defect IDs 1.0.1 and 1.0.2) and posts them.
- Build 1.1 is released. Testing defects 1.0.1 and 1.0.2 in this build is **re-testing**.

### Bug status flow
New/Open -> Assigned -> Fixed/Resolved -> Retest -> Closed (or Reopened if it still fails).
Exact status names vary by tool (in Jira it is usually To Do -> In Progress -> Done).

---

## 3. Re-Testing vs Regression Testing

| | Re-Testing | Regression Testing |
|---|---|---|
| Purpose | Confirm the specific bug is fixed | Confirm nothing else broke |
| Test cases | The failed ones | Previously passed ones |
| Order | First | After re-testing |

### Example: Admin, Purchase, Finance
An application has three modules: **Admin, Purchase, Finance**. **Finance depends on Purchase.**

1. The tester finds a bug in the **Purchase** module and posts it.
2. The dev fixes it and releases a new build.
3. **Re-testing:** verify the Purchase bug is fixed.
4. **Regression testing:** test the **Finance** module, which depends on Purchase, to confirm its existing functionality still works and meets the client requirement.

| Module | Test | Why |
|---|---|---|
| Purchase (bug fixed here) | Re-testing | Confirm the bug is fixed |
| Finance (depends on Purchase) | Regression | Confirm the Purchase fix did not break it |

**Rule:** re-test the module where the bug was fixed; run regression on the modules that depend on it. The fixed module's other test cases are also worth running, since a fix can cause side effects in neighbouring features.

---

## 4. Smoke Testing
A quick, shallow round of testing on a **new build** to confirm it is **stable and testable** before further testing. Also called **Build Verification Testing (BVT)**.

- Broad but shallow: touches the main features at a basic level.
- Done on initial builds, and usually on every new build release.
- Not the same as end-to-end testing, which is much deeper.

**What is checked:**
1. The build installs/deploys properly (QA environment for web apps)
2. The application opens (e.g. the QA URL loads)
3. Clicks and actions respond
4. Navigation works between modules and pages
5. Inner pages and links open correctly
6. Basic login and dashboard access

**Result:** if it passes, the build is accepted for further testing. If it fails, the build is **rejected** and sent back to the dev team.

---

## 5. Sanity Testing
A quick check of the **main functionalities** of the application **without going deeper**, done on a **relatively stable build**.

- Example: after a fix in the payment module, complete a successful transaction and check that the digital slip is generated with the correct paid amount.
- If it passes, system/regression testing continues. If it fails, the build is rejected.

---

## 6. Smoke vs Sanity Testing
Both come into the picture **after build release**.

| | Smoke Testing | Sanity Testing |
|---|---|---|
| Purpose | Confirm the build received from dev is testable/stable | Check the main functionalities during the release phase, without going deeper |
| Performed by | Developers and testers | Testers alone |
| Build | May be stable or unstable | Relatively stable |
| Done on | Initial builds | Stable builds |
| Part of | Basic testing | Regression testing |
| Frequency | Usually on every new build release | Planned when there is not enough time for in-depth testing |

### Build flow diagram

| Build type | Check | If it passes | If it fails |
|---|---|---|---|
| Initial or unstable build | Smoke testing | System and/or regression testing | Build rejected |
| Stable build (Build 1, 2 ... N) | Sanity testing | System and/or regression testing | Build rejected |

A rejected build goes back to the dev team.

---

## 7. Workflow When a Build Arrives
1. Run **smoke testing** first. If it fails, reject the build.
2. **Re-test** the bugs fixed in this build.
3. Run **regression** on the impacted/related modules (identified in the impact analysis with the dev).
4. For regression, use **sanity-level checks** when time is short, and detailed regression cases when time permits.

## 8. Testing After Smoke and Sanity
- **Functional testing:** in-depth testing of each module against the requirements (FRS), at the system testing level.
- **End-to-end testing:** the complete flow across modules, from a real user's point of view.
- **Non-functional testing:** performance, security, compatibility etc., where applicable.
- **Regression testing:** repeated on every new build.

```
Smoke -> Sanity -> Functional (module by module) -> End-to-end flows -> Regression on later builds
```

---

## Interview Tips
- Re-testing and regression are different: re-testing confirms the specific bug fix, regression checks that nothing else broke. Re-testing comes first.
- Smoke checks the build, sanity checks the main functionality of a stable build.
- Use the Purchase/Finance example to explain regression: the module that depends on the changed one is where side effects show up.
- If asked how you choose between regression types: regional needs a good impact analysis with the dev, and full regression is safer when many modules changed.
