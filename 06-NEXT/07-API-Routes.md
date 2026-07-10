🔹 Route Handlers (API Routes)
Route Handlers allow you to create custom request handlers for a given route using the Web Request and Response APIs. These take the place of classic Node.js API development.

JavaScript
// app/api/status/route.js
import { NextResponse } from 'next/server';

// Handle HTTP GET requests
export async function GET() {
return NextResponse.json({
status: 'online',
timestamp: new Date().toISOString(),
environment: process.env.NODE_ENV
});
}

// Handle HTTP POST requests
export async function POST(request) {
const body = await request.json();
return NextResponse.json({ message: 'Data logged successfully', received: body }, { status: 201 });
}
