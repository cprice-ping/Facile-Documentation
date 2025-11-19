# Purpose
This is the documentation site for Project Facile - providing comprehensive guides, references, and resources for deploying and using PingIdentity CIAM solutions.

## Project 'Facile'

![facile qr](https://cdn.glitch.com/d73a8d8c-7227-47ee-8646-873dea902e5f%2Ffacile-qr.png?v=1613112549901)

1. Signup for My Ping
2. Go to [facile.pingidentity.cloud](https://facile.pingidentity.cloud)
3. You're done! How about that?

## Made By
Chris Price - cprice@pingidentity.com

## Contributors
* Arnaud Lacour - arno@pingidentity.com
* Samir Gandhi - samirgandhi@pingidentity.com

## Live Documentation

Visit the live documentation at: [https://cprice-ping.github.io/Facile-Documentation/](https://cprice-ping.github.io/Facile-Documentation/)

## Local Development

### Prerequisites
- Node.js 18+
- npm

### Setup and Run

```bash
# Install dependencies
npm install

# Start development server
npm start
```

The site will be available at `http://localhost:8080`

### Build for Production

```bash
# Build the static site
npm run build
```

The built site will be in the `build/` directory.

### Build for GitHub Pages

```bash
# Build with path prefix for GitHub Pages
npm run build-ghpages
```

## Deployment

This site automatically deploys to GitHub Pages via GitHub Actions when changes are pushed to the `main` branch.
