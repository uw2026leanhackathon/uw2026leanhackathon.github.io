<script lang="ts">
	const organizers = [
		{ name: 'Jarod Alper', department: 'Mathematics', role: 'Faculty', website: 'https://sites.math.washington.edu//~jarod/' },
		{ name: 'Gilbert Bernstein', department: 'PLSE', role: 'Faculty', website: 'http://gilbertbernstein.com/' },
		{ name: 'Dhruv Bhatia', department: 'Mathematics', role: 'PhD Student', website: 'https://dbhatia.xyz/' },
		{ name: 'Oliver Flatt', department: 'PLSE', role: 'PhD Student', website: 'https://www.oflatt.com/' },
		{ name: 'Vasily Ilin', department: 'Mathematics', role: 'PhD Student', website: 'https://vilin97.github.io/' },
		{ name: 'Eric Klavins', department: 'ECE', role: 'Faculty', website: 'https://klavinslab.org/people/Klavins.html' },
		{ name: 'Zachary Tatlock', department: 'PLSE', role: 'Faculty', website: 'https://ztatlock.net/' },
		{ name: 'Michael Zeng', department: 'Mathematics', role: 'PhD Student', website: 'https://zengrf.github.io' }
	];

	function getInitials(name: string): string {
		return name.split(' ').map(n => n[0]).join('');
	}

	function getDeptColor(dept: string): string {
		const colors: Record<string, string> = {
			'Mathematics': '#a87cff',
			'PLSE': '#f0cc5b',
			'ECE': '#7cf0b5'
		};
		return colors[dept] || '#8b54fa';
	}
</script>

<section id="organizers" class="section" style="position: relative; overflow: hidden;">
	<div class="container">
		<h2 class="section-title">Organizers & Sponsors</h2>

		<div class="organizers-grid">
			{#each organizers as person, i}
				<a href={person.website} target="_blank" rel="noopener" class="organizer-card glass-card linkable" style="animation-delay: {i * 0.08}s">
					<div class="avatar" style="border-color: {getDeptColor(person.department)}">
						<span class="avatar-initials" style="color: {getDeptColor(person.department)}">{getInitials(person.name)}</span>
					</div>
					<h3>{person.name}</h3>
					<span class="dept" style="color: {getDeptColor(person.department)}">{person.department}</span>
					<span class="role">{person.role}</span>
				</a>
			{/each}
		</div>

		<div class="sponsors-showcase">
			<div class="sponsor-card glass-card">
				<div class="sponsor-logo">
					<span class="sponsor-icon">⬡</span>
				</div>
				<h3>Amazon Automated Reasoning Group</h3>
				<p>Supporting advances in formal verification and proof automation.</p>
				<span class="badge badge-gold">Sponsor</span>

				<!-- Decorative Lean snippet -->
				<div class="floating-snippet snippet-cta">
					<pre><code><span class="kw">def</span> <span class="fn">fibonacci</span> : ℕ → ℕ
  | 0     => 0
  | 1     => 1
  | n + 2 => <span class="fn">fibonacci</span> n + <span class="fn">fibonacci</span> (n + 1)</code></pre>
				</div>
			</div>
		</div>

		<div class="cta-section">
			<div class="cta-card glass-card glow-purple">
				<h2>Ready to Prove Something Amazing?</h2>
				<p>
					Apply to join us May 8–10, 2026 at the University of Washington for two days of hacking,
					learning, and collaboration around the Lean Proof Assistant.
					Spaces are limited — applications will be reviewed by the organizing committee.
				</p>
				<div class="cta-actions">
					<a href="https://docs.google.com/forms/d/14MZXvEmHV1iRMvncWguiUfyeDJbYOFKQVbbDYiSkf6A" class="btn btn-primary" target="_blank" rel="noopener">
						Apply to Participate →
					</a>
					<a href="https://docs.google.com/forms/d/e/1FAIpQLSdI-axdDzcTjmWrBlEXj7tz_W2Pg0tPXZYhihYKa9ACW7pGRw/viewform?usp=publish-editor" class="btn btn-outline" target="_blank" rel="noopener">
						RSVP as Invited Guest
					</a>
				</div>
			</div>
		</div>

	</div>
</section>

<style>
	.organizers-grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
		gap: 1.25rem;
		margin-bottom: 4rem;
	}

	.organizer-card {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		padding: 2rem 1.5rem;
		animation: fadeInUp 0.6s ease both;
		text-decoration: none;
		color: inherit;
		cursor: pointer;
	}

	.avatar {
		width: 70px;
		height: 70px;
		border-radius: 50%;
		border: 2px solid;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 1rem;
		background: rgba(139, 84, 250, 0.08);
	}

	.avatar-initials {
		font-size: 1.3rem;
		font-weight: 700;
		font-family: var(--font-mono);
	}

	.organizer-card h3 {
		font-size: 1rem;
		color: var(--text-heading);
		margin-bottom: 0.3rem;
	}

	.dept {
		font-size: 0.8rem;
		font-weight: 600;
	}

	.role {
		font-size: 0.75rem;
		color: var(--text-muted);
		margin-top: 0.2rem;
	}

	.linkable:hover {
		border-color: rgba(139, 84, 250, 0.5);
		box-shadow: 0 20px 60px rgba(107, 63, 160, 0.2);
	}

	@keyframes fadeInUp {
		from {
			opacity: 0;
			transform: translateY(20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.sponsors-showcase {
		display: flex;
		justify-content: center;
		margin-bottom: 5rem;
	}

	.sponsor-card {
		position: relative;
		overflow: visible;
		text-align: center;
		padding: 3rem 4rem;
		max-width: 500px;
		background: linear-gradient(135deg, rgba(232, 185, 49, 0.05), rgba(139, 84, 250, 0.05));
		border-color: rgba(232, 185, 49, 0.2);
	}

	.sponsor-card:hover {
		border-color: rgba(232, 185, 49, 0.4);
	}

	.sponsor-logo {
		margin-bottom: 1.5rem;
	}

	.sponsor-icon {
		font-size: 4rem;
		color: var(--gold-400);
	}

	.sponsor-card h3 {
		font-size: 1.3rem;
		color: var(--text-heading);
		margin-bottom: 0.75rem;
	}

	.sponsor-card p {
		color: var(--text-muted);
		font-size: 0.95rem;
		margin-bottom: 1.25rem;
		line-height: 1.6;
	}

	.cta-section {
		margin-top: 2rem;
	}

	.cta-card {
		text-align: center;
		padding: 4rem 3rem;
		background: linear-gradient(135deg, rgba(139, 84, 250, 0.12), rgba(107, 63, 160, 0.06));
		border-color: rgba(139, 84, 250, 0.3);
	}

	.cta-card h2 {
		font-size: 2.2rem;
		margin-bottom: 1rem;
		background: linear-gradient(135deg, var(--purple-300), var(--gold-400));
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
	}

	.cta-card p {
		color: var(--text-muted);
		font-size: 1.1rem;
		max-width: 600px;
		margin: 0 auto 2rem;
		line-height: 1.7;
	}

	.cta-actions {
		display: flex;
		gap: 1rem;
		justify-content: center;
		flex-wrap: wrap;
	}

	.floating-snippet {
		position: absolute;
		background: rgba(139, 84, 250, 0.06);
		border: 1px solid rgba(139, 84, 250, 0.15);
		border-radius: 12px;
		padding: 1rem 1.25rem;
		font-family: 'JetBrains Mono', monospace;
		font-size: 0.8rem;
		color: var(--text-muted);
		pointer-events: none;
		z-index: 0;
		white-space: pre;
		line-height: 1.6;
	}

	.floating-snippet pre {
		margin: 0;
	}

	.floating-snippet code {
		font-family: inherit;
	}

	.floating-snippet .kw { color: var(--purple-300); }
	.floating-snippet .fn { color: var(--gold-400); }

	.snippet-cta {
		top: -1.5rem;
		right: -12rem;
		transform: rotate(1.5deg);
		opacity: 0.45;
	}

	@media (max-width: 768px) {
		.organizers-grid {
			grid-template-columns: repeat(2, 1fr);
		}
		.sponsor-card {
			padding: 2rem;
		}
		.floating-snippet {
			display: none;
		}
		.cta-card {
			padding: 3rem 1.5rem;
		}
		.cta-card h2 {
			font-size: 1.7rem;
		}
	}
</style>
