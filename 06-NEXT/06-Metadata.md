─── 2. Optimization & Back-End ───
🔹 Metadata
Next.js provides a built-in Metadata API to modify your application’s HTML <head> tags (crucial for SEO and social media sharing embeds). You can export static or dynamic metadata objects from any server layout or page file.

JavaScript
// app/about/page.js

// 1. Static Metadata
export const metadata = {
title: 'About Us | My Enterprise App',
description: 'Learn more about our core philosophy and global engineering team.',
};

export default function AboutPage() {
return <h1>About Page</h1>;
}
