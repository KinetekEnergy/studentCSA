---
layout: blogs
title: 
description: Home Page
hide: true
---


<style>
    #github-stats {
        text-align: center;
        padding: 20px;
        border-radius: 4px;
        background-color: #1e1e1e;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    .stat {
        display: inline-block;
        margin: 0 10px;
    }

    .separator {
        margin: 0 10px;
        color: #666;
    }

    .title {
        text-align: center;
        font-weight: 1000;
        font-size: 25px;
    }

</style>

<body>
    <div id="github-stats" class="glow-on-hover-search">
        <p class="title">GitHub Stats</p>
        <div id="stats-container">
            <span class="stat">Issues: <span id="issues">Loading...</span></span>
            <span class="separator">|</span>
            <span class="stat">Pull Requests: <span id="pull-requests">Loading...</span></span>
            <span class="separator">|</span>
            <span class="stat">Commits: <span id="commits">Loading...</span></span>
            <span class="separator">|</span>
            <span class="stat">Public Repos: <span id="public-repos">Loading...</span></span>
            <span class="separator">|</span>
            <span class="stat">Followers: <span id="followers">Loading...</span></span>
        </div>
    </div>
    
    <script>
        const username = 'KinetekEnergy';

        async function fetchData(url) {
            const response = await fetch(url);
            return response.json();
        }

        async function updateStats() {
            try {
                const userResponse = await fetchData(`https://api.github.com/users/${username}`);
                document.getElementById('public-repos').textContent = userResponse.public_repos;
                document.getElementById('followers').textContent = userResponse.followers;

                const reposResponse = await fetchData(userResponse.repos_url);
                let totalIssues = 0;
                let totalPullRequests = 0;
                let totalCommits = 0;

                for (const repo of reposResponse) {
                    const issuesResponse = await fetchData(`${repo.url}/issues?state=all`);
                    totalIssues += issuesResponse.length;

                    const pullsResponse = await fetchData(`${repo.url}/pulls?state=all`);
                    totalPullRequests += pullsResponse.length;

                    const commitsResponse = await fetchData(`${repo.url}/commits`);
                    totalCommits += commitsResponse.length;
                }

                document.getElementById('issues').textContent = totalIssues;
                document.getElementById('pull-requests').textContent = totalPullRequests;
                document.getElementById('commits').textContent = totalCommits;
            } catch (error) {
                console.error('Error fetching GitHub data:', error);
            }
        }

        updateStats();
    </script>
</body>