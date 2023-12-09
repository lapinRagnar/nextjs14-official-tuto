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

### c.  Creating the dashboard pages
Let's practice creating more routes. In your dashboard, create two more pages:

Customers Page: The page should be accessible on http://localhost:3000/dashboard/customers. For now, it should return a `<p>Customers Page</p>` element.
Invoices Page: The invoices page should be accessible on http://localhost:3000/dashboard/invoices. For now, also return a `<p>Invoices Page</p> `element.


### d. Creating the dashboard layout
Dashboards have some sort of navigation that is shared across multiple pages. In Next.js, you can use a special layout.tsx file to create UI that is shared between multiple pages. Let's create a layout for the dashboard pages!

Inside the /dashboard folder, add a new file called layout.tsx and paste the following code:



> /app/dashboard/layout.tsx
```{.typescript .numberLines .lineAnchors } 

import SideNav from '@/app/ui/dashboard/sidenav';
 
export default function Layout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen flex-col md:flex-row md:overflow-hidden">
      <div className="w-full flex-none md:w-64">
        <SideNav />
      </div>
      <div className="flex-grow p-6 md:overflow-y-auto md:p-12">{children}</div>
    </div>
  );
}

```


One benefit of using layouts in Next.js is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering:

![Alt text](image-1.png)



## 5. Navigating Between Pages


### a. The <Link> component


> /app/ui/dashboard/nav-links.tsx
```{.typescript .numberLines .lineAnchors highlight=[7, 17, 24]} 


import {
  UserGroupIcon,
  HomeIcon,
  DocumentDuplicateIcon,
} from '@heroicons/react/24/outline';
import Link from 'next/link';
 
// ...
 
export default function NavLinks() {
  return (
    <>
      {links.map((link) => {
        const LinkIcon = link.icon;
        return (
          <Link
            key={link.name}
            href={link.href}
            className="flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3"
          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
        );
      })}
    </>
  );
}


```

### b. Pattern: Showing active links

A common UI pattern is to show an active link to indicate to the user what page they are currently on. To do this, you need to get the user's current path from the URL. Next.js provides a hook called usePathname() that you can use to check the path and implement this pattern.

Since ``usePathname()`` is a hook, you'll need to turn nav-links.tsx into a Client Component. Add React's `"use client"` directive to the top of the file, then import ```usePathname()``` from next/navigation:




> /app/ui/dashboard/nav-links.tsx
```{.typescript .numberLines .lineAnchors highlight=[1, 8]} 

'use client';
 
import {
  UserGroupIcon,
  HomeIcon,
  InboxIcon,
} from '@heroicons/react/24/outline';
import Link from 'next/link';
import { usePathname } from 'next/navigation';
 
// ...

```

Next, assign the path to a variable called pathname inside your <NavLinks /> component:



> /app/ui/dashboard/nav-links.tsx
```{.typescript .numberLines .lineAnchors highlight=[2]} 

export default function NavLinks() {
  const pathname = usePathname();
  // ...
}
```

You can use the clsx library introduced in the chapter on CSS styling to conditionally apply class names when the link is active. When link.href matches the pathname, the link should displayed with blue text and a light blue background.

Here's the final code for nav-links.tsx:

> /app/ui/dashboard/nav-links.tsx
```{.typescript .numberLines .lineAnchors highlight=[10, 25-30]} 

'use client';
 
import {
  UserGroupIcon,
  HomeIcon,
  DocumentDuplicateIcon,
} from '@heroicons/react/24/outline';
import Link from 'next/link';
import { usePathname } from 'next/navigation';
import clsx from 'clsx';
 
// ...
 
export default function NavLinks() {
  const pathname = usePathname();
 
  return (
    <>
      {links.map((link) => {
        const LinkIcon = link.icon;
        return (
          <Link
            key={link.name}
            href={link.href}
            className={clsx(
              'flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3',
              {
                'bg-sky-100 text-blue-600': pathname === link.href,
              },
            )}
          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
        );
      })}
    </>
  );
}

```

Save and check your localhost. You should now see the active link highlighted in blue.

___

## 6. Setting Up Your Database

Before you can continue working on your dashboard, you'll need some data. In this chapter, you'll be setting up a PostgreSQL database using @vercel/postgres.

### a. Create a GitHub repository
To start, let's push your repository to Github if you haven't done so already. This will make it easier to set up your database and deploy.

### b. Create a Vercel account

### c. Connect and deploy your project

Next, you'll be taken to this screen where you can select and import the GitHub repository you've just created:
![Alt text](image-2.png)

Name your project and click Deploy.
![Alt text](image-3.png)

Hooray! 🎉 Your project is now deployed.
![Alt text](image-4.png)

By connecting your GitHub repository, whenever you push changes to your main branch, Vercel will automatically redeploy your application with no configuration needed. When opening pull requests, you'll also have instant previews which allow you to catch deployment errors early and share a preview of your project with team members for feedback.


### d. Create a Postgres database
Next, to set up a database, click Continue to Dashboard and select the Storage tab from your project dashboard. Select Connect Store → Create New → Postgres → Continue.

![Alt text](image-5.png)

Once connected, navigate to the .env.local tab, click Show secret and Copy Snippet. Make sure you reveal the secrets before copying them.

![Alt text](image-6.png)

Navigate to your code editor and rename the .env.example file to .env. Paste in the copied contents from Vercel.

Important: Go to your .gitignore file and make sure .env is in the ignored files to prevent your database secrets from being exposed when you push to GitHub.

Finally, run 
```cmd
npm i @vercel/postgres 
```

in your terminal to install the Vercel Postgres SDK.


### e. Seed your database

Now that your database has been created, let's seed it with some initial data. This will allow you to have some data to work with as you build the dashboard.

In the /scripts folder of your project, there's a file called seed.js. This script contains the instructions for creating and seeding the invoices, customers, user, revenue tables.

Don't worry if you don't understand everything the code is doing, but to give you an overview, the script uses SQL to create the tables, and the data from placeholder-data.js file to populate them after they've been created.

Next, in your package.json file, add the following line to your scripts:


> /package.json
```{.typescript .numberLines .lineAnchors highlight=[5]} 
"scripts": {
  "build": "next build",
  "dev": "next dev",
  "start": "next start",
  "seed": "node -r dotenv/config ./scripts/seed.js"
},


```

puis,

Now, run npm run seed. You should see some console.log messages in your terminal to let you know the script is running.

```cmd
npm run seed
```

### f. Exploring your database
Let's see what your database looks like. Go back to Vercel, and click Data on the sidenav.

In this section, you'll find the four new tables: users, customers, invoices, and revenue.
![Alt text](image-7.png)


### g. Executing queries
You can switch to the "query" tab to interact with your database. This section supports standard SQL commands. For instance, inputting DROP TABLE customers will delete "customers" table along with all its data - so be careful!

Let's run your first database query. Paste and run the following SQL code into the Vercel interface:

```sql
SELECT invoices.amount, customers.name
FROM invoices
JOIN customers ON invoices.customer_id = customers.id
WHERE invoices.amount = 666;
```















***







# Autre ressources
## pour markdown syntaxe
https://shd101wyy.github.io/markdown-preview-enhanced/#/markdown-basics?id=line-numbers
https://www.markdownguide.org/basic-syntax/

## astuce et raccourcis clavier markdown
https://thinkr.fr/r-markdown-les-petits-trucs-qui-changent-la-vie/

