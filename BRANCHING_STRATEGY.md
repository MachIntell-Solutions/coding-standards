Markdown
# Git Branching Strategy
We use the following Git branch structure:

main  
├── develop  
├── feature/  
├── bugfix/  
├── hotfix/  
└── release/


---

## 1. Main Branch

**Branch:** `main`

The `main` branch contains the stable production code.

* Only tested and approved code should be merged here.
* Do not develop directly on `main`.
* Every production release should have a version tag.

**Example:** 

main  
└── v1.0.0


---

## 2. Develop Branch

**Branch:** `develop`

The `develop` branch contains the latest development code.

* Features are merged here after development.
* Development bug fixes are merged here.
* It may contain code that is not yet ready for production.
* Do not develop directly on `develop`.

**Example:**  

develop  
├── feature/login  
├── feature/payment  
└── bugfix/order-total  


---

## 3. Feature Branch

**Branch:** `feature/<short-description>`

Use a feature branch when you are adding a new feature.

* **Source:** Create it from `develop`.

**Examples:**
* `feature/user-login`
* `feature/payment`
* `feature/order-history`

**Flow:**  

develop  
│
└── feature/user-login  
│
└──> develop


> After the feature is completed and tested, create a Pull Request and merge it into `develop`.

---

## 4. Bugfix Branch

**Branch:** `bugfix/<short-description>`

Use a bugfix branch when you find a bug during development or testing.

* **Source:** Create it from `develop`.

**Examples:**
* `bugfix/login-validation`
* `bugfix/incorrect-total`
* `bugfix/order-status`

**Flow:**  

develop  
│
└── bugfix/incorrect-total  
│
└──> develop. 


> After fixing and testing the bug, create a Pull Request and merge it into `develop`.

---

## 5. Release Branch

**Branch:** `release/<version>`

Use a release branch when the features for a version are ready and you want to prepare the application for production.

* **Source:** Create it from `develop`.

**Examples:**
* `release/1.0.0`
* `release/1.1.0`
* `release/2.0.0`

**During the release stage:**
* Test the application.
* Fix release-related bugs.
* Update the version.
* Update release documentation.
* **Do not** add new features.

**Flow:**  
develop  
│
└── release/1.0.0  
│
├──> main  
│
└──> develop  


> After the release is approved, merge it into both `main` and `develop`. Then create a version tag on `main`.

main   
└── v1.0.0


---

## 6. Hotfix Branch

**Branch:** `hotfix/<short-description>`

Use a hotfix branch when there is a serious problem in production that needs to be fixed immediately.

* **Source:** Create it from `main`.

**Examples:**
* `hotfix/payment-failure`
* `hotfix/login-crash`
* `hotfix/security-issue`

**Flow:**
main  
│
└── hotfix/payment-failure  
│
├──> main  
│
└──> develop 


> The hotfix should be merged into both:
> 1. `main` → to fix the production problem
> 2. `develop` → so the same fix is included in future releases

---

## Branch Summary

| Branch | Purpose |
| :--- | :--- |
| `main` | Stable production code |
| `develop` | Latest development code |
| `feature/*` | New features |
| `bugfix/*` | Bugs found during development |
| `release/*` | Preparing a release |
| `hotfix/*` | Urgent production fixes |

---

## Simple Workflow

### New Feature
develop  
↓  
feature/login  
↓  
develop


### Development Bug
develop  
↓  
bugfix/login-error  
↓  
develop


### New Release
develop  
↓  
release/1.0.0  
↓  
main (also merge back into develop)


### Production Bug
main  
↓  
hotfix/payment-error  
↓  
main (also merge back into develop)


---

## Important Rules

1. **Do not directly push to `main`.**
2. **Do not directly push to `develop`.**
3. **Use Pull Requests** for merging.
4. **Test your changes** before creating a Pull Request.
5. **Use meaningful branch names.**
6. **Delete `feature` and `bugfix` branches** after they are merged.
7. **Hotfixes must be merged into both `main` and `develop`.**
8. **Release branches are for testing and final preparation**, not for adding new features.

---

## Branch Naming Examples

* **Features:** `feature/user-login`, `feature/payment-gateway`
* **Bugfixes:** `bugfix/login-validation`, `bugfix/incorrect-total`
* **Hotfixes:** `hotfix/payment-failure`, `hotfix/production-crash`
* **Releases:** `release/1.0.0`, `release/1.1.0`

---

## In Simple Words

* `main` → Production code
* `develop` → Development code
* `feature` → New feature
* `bugfix` → Fix development bug
* `release` → Prepare a new version
* `hotfix` → Fix urgent production bug