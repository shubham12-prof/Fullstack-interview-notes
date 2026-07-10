🔹 Middleware
Middleware allows you to run custom code before a request is completed. You can intercept requests and responses, rewrite paths, redirect users, or validate authentication tokens. It is defined in a single middleware.js file at the root level.

JavaScript
// middleware.js
import { NextResponse } from 'next/server';

export function middleware(request) {
const token = request.cookies.get('session-token');

// If the user tries to access the dashboard without a valid token, redirect to login
if (request.nextUrl.pathname.startsWith('/dashboard') && !token) {
return NextResponse.redirect(new URL('/login', request.url));
}

return NextResponse.next();
}

// Config targets middleware to only run on specific route matching configurations
export const config = {
matcher: '/dashboard/:path\*',
};
