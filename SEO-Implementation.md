# SEO Implementation Documentation - BabyMD

This document outlines the SEO strategies & technical implementations currently in place for the BabyMD Next.js project.

## 1. Metadata Management
The project utilizes the Next.js `Metadata` API for both global and page-specific SEO tags.

- **Global Metadata**: Defined in the root `layout.tsx`, providing default titles and descriptions.
- **Page-Specific Metadata**: Each major page (Home, About, Clinics, Services, etc.) has a dedicated `metadata` object that overrides global defaults with highly optimized keywords.
- **Canonical URLs**: Implemented via `alternates.canonical` in the metadata of each page to prevent duplicate content issues.
- **Dynamic Metadata**: For dynamic routes like doctor profiles and clinic pages, metadata is generated dynamically based on the specific entity being viewed.

## 2. Breadcrumbs
Breadcrumbs are implemented both visually and semantically to enhance navigation and search engine understanding.

- **UI Component**: A reusable `Breadcrumb.tsx` component is used across the site to provide clear navigational paths for users.
- **Semantic Implementation**: Every major route includes a `BreadcrumbList` JSON-LD schema, helping search engines display rich breadcrumb snippets in Search Results.
- **Dedicated Utilities**: Breadcrumb schemas are managed via centralized utilities:
  - `src/utils/generalBreadcrumbSchemas.ts`
  - `src/utils/clinicBreadcrumbSchemas.ts`
  - `src/utils/breadcrumbSchemas.ts` (for doctors)

## 3. OpenGraph & Social Media
The project is fully optimized for social sharing with comprehensive OpenGraph (OG) and Twitter card support.

- **OG Tags**: Included in the `metadata` object of pages, covering `og:title`, `og:description`, `og:url`, `og:site_name`, and `og:type`.
- **Social Images**: High-quality, optimized OG images (minified for performance) are specifically assigned to different sections of the site.
- **Twitter Cards**: Configured with `summary_large_image` to ensure rich previews on Twitter/X.

## 4. Structured Data (JSON-LD Schemas)
A wide array of schema types is implemented to provide search engines with deep context about the business, its services, and its staff.

- **Organization & MedicalOrganization**: Defines the core business entity, including logo, founding date, area served, and funding information.
- **WebSite**: Provides search engines with the official site name and URL.
- **LocalBusiness**: Specifically targets local SEO for the Bangalore region, including physical address and contact details.
- **Physician Schema**: Each doctor profile includes a dedicated `Physician` schema with details on medical specialty, qualifications, languages known, and experience.
- **BreadcrumbList**: (As mentioned above) provides hierarchical navigation context.

## 5. Sitemap
The project uses a dynamic sitemap generation strategy to ensure all active pages are indexed.

- **Location**: `src/app/sitemap.xml/route.ts`
- **Functionality**: Dynamically generates an XML sitemap including:
  - Static core pages (Home, About, Services, Contact)
  - Clinic location pages
  - Individual doctor profile pages
  - Detailed service sub-pages
- **Frequency**: Uses `lastmod` tags to inform search engines about the last update of each URL.

## 6. Robots Configuration
The `robots.ts` file manages search engine crawling behavior to prioritize production content and hide internal or staging environments.

- **Location**: `src/app/robots.ts`
- **Key Rules**:
  - **Disallows**: Staging URLs, development environments, internal patient portal routes (`/pp/*`), lead forms (`/form/*`), and legacy blog paths.
  - **Sitemap Link**: Explicitly points crawlers to the dynamic sitemap index.

## 7. Performance & SEO Best Practices
Technical SEO is further bolstered by performance optimizations:

- **Next.js Font Optimization**: Uses `next/font/google` with preloading to prevent layout shifts (CLS) and improve page speed.
- **Resource Hints**: Implements `preconnect` for Google Fonts and VWO to reduce latency for external assets.
- **Semantic HTML**: Extensive use of semantic tags (`<main>`, `<section>`, `<h1>`-`<h6>`) to ensure clear document hierarchy.
- **Google Tag Manager**: Integrated via `@next/third-parties/google` for efficient tracking and analytics without sacrificing performance.
