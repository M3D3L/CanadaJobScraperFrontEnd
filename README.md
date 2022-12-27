<h1>Job Listing App</h1>

<p>This is a Nuxt.js application that displays a list of job openings using scraped data from <a href="https://github.com/M3D3L/CanadaJobScraper" target="_blank">Canada Job Scraper</a>. It includes a search bar to filter the list of jobs.</p>

<h2>Live Version</h2>

<a href="https://charming-biscochitos-7f40df.netlify.app/" target="_blank">View Live Version</a>

<h2>Requirements</h2>

<p>Node and npm (comes with node)</p>

<h2>Npm commands</h2>
<ul>
<li>
npm install: installs the required modules
</li>
<li>
npm run dev: runs the program
</li>
<li>
npm generate: builds the project.
</li>
</ul>

<h2>Components</h2>

<p>The app consists of the following components:</p>

<ul>
  <li><code>MetaData</code>: This component is responsible for adding metadata to the page such as the page title and description.</li>
  <li><code>BaseHeader</code>: This component displays the search bar and emits events when the search input is updated or reset.</li>
  <li><code>JobList</code>: This component displays the list of jobs and receives the list of jobs as a prop.</li>
  <li><code>BaseFooter</code>: This component displays the current year and is only shown if there are more than 4 jobs in the list.</li>
</ul>

<h2>Data</h2>

<p>The job data is imported from a JSON file called <code>data.json</code> and stored in the <code>jobs</code> data property. A backup of the original data is also stored in the <code>backup</code> data property to allow for resetting the search results.</p>

<h2>Animations</h2>

<p>The app includes animations for the header and the list items. The header fades in and out on scroll and the list items fade in when they becomes visible. These animations are implemented using intersection observers.</p>

<h2>CSS</h2>

<p>The app uses CSS variables and the <code>@apply</code> directive from <a href="https://tailwindcss.com/">Tailwind CSS</a> to style the components. The app also includes a custom scrollbar style for Firefox, Chrome, Edge, and Safari.</p>

<p>The job data is imported from a JSON file called <code>data.json</code> and stored in the <code>jobs</code> data property. A backup of the original data is also stored in the <code>backup</code> data property to allow for resetting the search results.</p>