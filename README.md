## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

___

## 1 getting started
### 1.1. installation du projet etinstall dependencies
```bash
npx create-next-app@latest nextjs-dashboard --use-npm --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example"
```

### 1.2 configurer typescipt avec vscode

![Alt text](image.png)

___

## 2 css styling
### 2.1. comment ajouter un css tailwind
  voir code
### 2.2. comment ajouter un css module
  voir code
### 2.3. Using the clsx library to toggle class names
  https://github.com/lukeed/clsx

___

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


### 3.3 Optimizing Images

> /app/page.tsx
```{.typescript .numberLines .lineAnchors highlight=[5,12-18]} 

  import AcmeLogo from '@/app/ui/acme-logo';
  import { ArrowRightIcon } from '@heroicons/react/24/outline';
  import Link from 'next/link';
  import { lusitana } from '@/app/ui/fonts';
  import Image from 'next/image';
  
  export default function Page() {
    return (
      // ...
      <div className="flex items-center justify-center p-6 md:w-3/5 md:px-28 md:py-12">
        {/* Add Hero Images Here */}
        <Image
          src="/hero-desktop.png"
          width={1000}
          height={760}
          className="hidden md:block"
          alt="Screenshots of the dashboard project showing desktop version"
        />
      </div>
      //...
    );
  }

```

### 3.4 Lecture 
  - Image Optimization Docs : https://nextjs.org/docs/app/building-your-application/optimizing/images
  - Font Optimization Docs : https://nextjs.org/docs/app/building-your-application/optimizing/fonts
  - Improving Web Performance with Images (MDN) : https://developer.mozilla.org/en-US/docs/Learn/Performance/Multimedia
  - Web Fonts (MDN) : https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts


___

## 4. Creating Layouts and Pages

### a. Creating the dashboard page
Create a new folder called dashboard inside /app. Then, create a new page.tsx file inside the dashboard folder with the following content:


> /app/dashboard/page.tsx
```{.typescript .numberLines .lineAnchors highlight=[5,12-18]} 

  export default function Page() {
    return <p>Dashboard Page</p>;
  }

```

### b. ensuite on peut visiter le lien
> http://localhost:3000/dashboard

This is how you can create different pages in Next.js: create a new route segment using a folder, and add a page file inside it.


By having a special name for page files, Next.js allows you to colocate UI components, test files, and other related code with your routes. Only the content inside the page file will be publicly accessible. For example, the /ui and /lib folders are colocated inside the /app folder along with your routes.














***


# Autre ressources
## pour markdown syntaxe
https://shd101wyy.github.io/markdown-preview-enhanced/#/markdown-basics?id=line-numbers
https://www.markdownguide.org/basic-syntax/

## astuce et raccourcis clavier markdown
https://thinkr.fr/r-markdown-les-petits-trucs-qui-changent-la-vie/

