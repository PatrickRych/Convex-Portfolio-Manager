# Uploading this project to GitHub

You do **not** need the command line for the first upload.

## 1. Open your empty repository

Go to the `convex-portfolio-manager` repository you already created.

## 2. Upload the package contents

Click **Add file → Upload files**.

Open the unzipped `convex-portfolio-manager` folder on your computer and drag **the contents inside it** into the GitHub upload area:

- `README.md`
- `.gitignore`
- `demo/`
- `docs/`
- `images/`

Do not drag the outer folder itself if GitHub would create another nested `convex-portfolio-manager/convex-portfolio-manager/` directory.

## 3. Commit

At the bottom of the upload page, use a commit message such as:

```text
Initial CONVEX portfolio project
```

Then click **Commit changes**.

## 4. Check the front page

GitHub should automatically render `README.md` underneath the file list. Confirm that:

- the hero Risk Manager image loads
- the other screenshots load
- the demo workbook link opens the Excel file
- the `docs` links work

## 5. Do not upload the private workbook

Keep these files off the public repository:

- the original `.xlsb`
- the private `.xlsx` copy
- unredacted screenshots
- live brokerage exports
- Options Samurai cached values / licensed datasets

The repository should contain only the sanitized files in this package.
