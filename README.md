## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## 1 getting started
### 1.1. installation du projet etinstall dependencies
```bash
npx create-next-app@latest nextjs-dashboard --use-npm --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example"
```

### 1.2 configurer typescipt avec vscode

![Alt text](image.png)


## 2 css styling
### 2.1. comment ajouter un css tailwind
  voir code
### 2.2. comment ajouter un css module
  voir code
### 2.3. Using the clsx library to toggle class names
  https://github.com/lukeed/clsx

## 3. Optimizing Fonts and Images
### 3.1. pour mesurer l'efficacité de font
  https://web.dev/articles/cls?hl=fr

### 3.2. Adding a primary font
 - creer un fichier : /app/ui/font.ts
 - avec :

```ts
  import { Inter } from 'next/font/google';
  export const inter = Inter({ subsets: ['latin'] });
```

 - Finally, add the font to the <body> element in /app/layout.tsx:

  la classe : className={`${inter.className} antialiased`}

```{.typescript .numberLines .lineAnchors highlight=[2,11]} 
  import '@/app/ui/global.css';
  import { inter } from '@/app/ui/fonts' 
  
  export default function RootLayout({
    children,
  }: {
    children: React.ReactNode;// nouveau
  }) {
    return (
      <html lang="en">
        <body className={`${inter.className} antialiased`}>{children}</body>  // nouveau
      </html>
    );
  }

```

### 3.2. Adding a secondary font
 - voir les codes
 - comment faire :
https://nextjs.org/docs/app/building-your-application/optimizing/fonts#using-multiple-fonts

 - liste des toutes les options
https://nextjs.org/docs/app/api-reference/components/font#font-function-arguments




# Autre ressources
## pour markdown syntaxe
https://shd101wyy.github.io/markdown-preview-enhanced/#/markdown-basics?id=line-numbers

