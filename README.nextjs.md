# NextJs setup and Deployment

```
$ npm install -D @fullhuman/postcss-purgecss
```

## Production css setup

[stackoverflow.com](https://stackoverflow.com/questions/61325859/nextjs-tailwindcss-css-classes-are-missing-in-production)

```

// postcss.config.js

module.exports = {
   plugins: {
      tailwindcss: {},
      autoprefixer: {},
      ...(process.env.NODE_ENV === 'production'
         ? {
              '@fullhuman/postcss-purgecss': {
                 content: ['./components/**/*.js', './pages/**/*.js'],
                 defaultExtractor: content =>
                    content.match(/[\w-/:]+(?<!:)/g) || [],
              },
           }
         : {}),
   },
}
 - content is the path to add all your folders

```

## Tailwind.config.js setup

```
const defaultTheme = require('tailwindcss/defaultTheme');

module.exports = {
	purge: ['./pages/**/*.{js,ts,jsx,tsx}', './component/**/*.{js,ts,jsx,tsx}'],
	darkMode: 'class', // or 'media' or 'class'
	future: {
		removeDeprecatedGapUtilities: true,
	},
	theme: {
		extend: {
			fontFamily: {
				sans: ['Plain Light'],
			},
		},
		screens: {
			...defaultTheme.screens,
		},
		colors: {
			main: '#e4ff00',
			...defaultTheme.colors,
		},
	},
	variants: {
		extend: {},
	},
	plugins: [],
};

```

### Deploy to netlify

- create a netlify app
- deploy in main root directory else it will not work for nested folders

```
npm run build

npm run start // check for error first
```
