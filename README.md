# Shen Fang — Academic Website

This repository contains the source for Shen Fang's academic website, built with the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template.

## Local preview

```bash
bundle install
bundle exec jekyll serve -l -H localhost
```

Then open `http://localhost:4000`.

## Markdown 公式书写规范

Jekyll 会先用 Kramdown 解析 Markdown，再由 MathJax 渲染公式。因此，公式必须先避免被 Markdown 误解析。

- 行内公式使用 `$...$`，例如：`$E=mc^2$`。
- 行间公式的 `$$` 必须独占一行，并在公式块前后留空行：

  ```markdown
  $$
  E = mc^2
  $$
  ```

- 不要写成 `$$E=mc^2$$`，否则 Kramdown 可能将其当作行内公式，导致不换行或不居中。
- 行内公式中的 `_`、`*` 和 `|` 可能被 Markdown 当作强调或表格语法。遇到冲突时使用：
  - `_ {ij}` 表示下标；
  - `^{\ast}` 表示星号上标；
  - `\vert` 或 `\lvert...\rvert` 表示竖线。
- 不要使用 `\sb`，当前 MathJax 配置不能可靠渲染它。
- 修改 `_config.yml` 或 MathJax 配置后，需要重启 Jekyll，并在浏览器中使用 `Command + Shift + R` 强制刷新。
- 验证时不能只看 `jekyll build` 是否成功，还应在浏览器中确认行内公式和居中行间公式都已实际渲染。

## Publishing

Create a GitHub repository named `Eureka10shen.github.io`, add it as `origin`, and push the current branch. GitHub Pages will build and publish the site at `https://eureka10shen.github.io`.

```bash
git remote add origin https://github.com/Eureka10shen/Eureka10shen.github.io.git
git push -u origin master
```

The original Academic Pages repository is retained as the `upstream` remote for future template updates.

## Content locations

- `_pages/about.md`: homepage biography
- `_pages/research.md`: research overview
- `_pages/cv.md`: web CV
- `_publications/`: publication entries
- `images/profile.jpg`: profile photo
- `_config.yml`: site identity and links
- `_data/navigation.yml`: top navigation

Before publishing, review all content for privacy and accuracy. The current web CV intentionally excludes phone number, date of birth, political status, and other private fields.
