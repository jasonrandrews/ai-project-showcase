# AI Project Showcase

This is a project showcase website built with Astro. Each card on the home page represents a project that was created or improved using AI developer tools (such as GitHub Copilot, Amazon Q, or similar). Clicking a card opens a detailed page about that project, including the challenge, solution, results, and links to more information.

https://ai-project-showcase.netlify.app/

## 🚀 Running Locally

To run the project locally:

```sh
npm install
npm run dev
```

Then open [http://localhost:4321](http://localhost:4321) in your browser.

## 📝 Adding a New Project Card

To add your own project to the showcase:

1. Create a new Markdown file in `src/pages/projects/` (for example, `my-project.md`).
2. Use the following frontmatter at the top of your file:

   ```markdown
   ---
   layout: ../../layouts/ProjectLayout.astro
   title: "Your Project Title"
   summary: "A short summary of your project."
   author: "Your Name"
   ---
   ```
3. Write your project details below the frontmatter. You can use Markdown for formatting, images, and tables.
4. Save the file. Your project will automatically appear as a card on the home page, and visitors can click to view the full details.

For more contribution guidelines, see [CONTRIBUTING.md](CONTRIBUTING.md).

## 📁 Project Structure

- `src/pages/index.astro` — Home page with the project card grid
- `src/pages/projects/*.md` — Markdown files for each project
- `src/layouts/ProjectLayout.astro` — Shared layout for project detail pages
- `src/styles/global.css` — Global styles

## 🧞 Useful Commands

| Command         | Action                                    |
| :--------------| :-----------------------------------------|
| `npm install`  | Installs dependencies                     |
| `npm run dev`  | Starts local dev server at `localhost:4321`|
| `npm run build`| Build your production site to `./dist/`    |
| `npm run preview`| Preview your build locally               |

## 👀 Learn More

- [Astro Documentation](https://docs.astro.build)
- [Astro Discord](https://astro.build/chat)
