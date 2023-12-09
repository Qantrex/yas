# YAS - Yet Another Startpage

YAS is a simple and customizable start page built with Vue.js It features a minimalistic design with a search bar, quick links, a terminal, and a custom cursor. YAS allows you to personalize your start page experience with ease.

## Features

- **Search Bar**: Perform quick searches using your preferred search engine.
- **Quick Links**: Categorize and access your favorite links easily.
- **Color Picker**: Customize the accent color of the page to suit your style.
- **Custom Cursor**: Adds a unique touch with a customizable cursor.
- **Terminal**: Execute various commands directly from the start page.

## Getting Started

1. Clone the repository:
``` bash
git clone https://github.com/Qantrex/yas.git cd yas
```
2. Install adn fund dependencies:
``` bash
npm install
npm fund
```
3. Run the development server:
``` bash
npm run dev
```
4. After you finished with all your personalization you can follow [THIS](https://www.youtube.com/watch?v=yo2bMGnIKE8&t=159s) Guide on how to host the StartPage with Github Pages

## Usage

- **Search Bar**: Type your query and press Enter to perform a search using the selected search engine.
- **Quick Links**: Customize the links in the `QuickLinks.vue` component to suit your preferences.
- **Color Picker**: Click the color dot in the bottom right to open the color picker and choose your preferred accent color.
- **Terminal**: Press `:` to open the terminal. Use commands like `q` to close the terminal, `calc 1 + 1` for simple calculations, and more.

## Customize

You can modify the default accent color by changing the `--accent-color` variable in the `App.vue` file.
``` css
/* Light Blue Accent Color */
:root {
	--accent-color: #00bcd4;   
	--cursor-color: #ffffff; 
}
```

## Contributions

Contributions are welcome! If you have any ideas for improvement or new features, feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE.md](https://chat.openai.com/c/LICENSE.md) file for details.
