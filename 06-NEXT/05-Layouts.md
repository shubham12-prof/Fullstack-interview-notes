🔹 Layouts
A layout is UI that is shared between multiple pages. On navigation, layouts preserve state, remain interactive, and do not re-render. Layouts accept a children prop which injects child segments/pages.

JavaScript
// app/dashboard/layout.js
export default function DashboardLayout({ children }) {
return (

<div style={{ display: 'flex', minHeight: '100vh' }}>
{/_ Shared Sidebar across all dashboard routes _/}
<aside style={{ width: '250px', background: '#222', color: '#fff', padding: '20px' }}>
<h3>📊 Navigation</h3>
<ul>
<li>Analytics</li>
<li>Settings</li>
</ul>
</aside>

      {/* Nested page content will render here */}
      <main style={{ flex: 1, padding: '30px' }}>
        {children}
      </main>
    </div>

);
}
