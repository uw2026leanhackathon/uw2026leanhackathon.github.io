<script lang="ts">
	import firstPlacePhoto from '$lib/assets/1st_place.jpg';
	import secondPlacePhoto from '$lib/assets/2nd_place.jpg';
	import thirdPlacePhoto from '$lib/assets/3rd_place.jpg';

	const winningProjects = [
		{
			placement: '1st Place',
			project: 'cat-rw',
			tagline: 'A category-theoretic rewrite tactic for Lean 4.',
			description:
				'Brings category-theoretic rewriting to Lean 4 with `cat_rw`, letting users rewrite objects, goals, and propositions using isomorphisms.',
			link: 'https://github.com/leomayer1/cat-rw',
			team: ['Leopold Mayer', 'Grant Yang', 'Brian Nugent'],
			highlight: 'gold',
			image: firstPlacePhoto,
			imageAlt: 'First place winners posing with the cat-rw project award'
		},
		{
			placement: '2nd Place',
			project: 'Learned Tactic Branching',
			tagline: 'Neural-guided automated proof search for Lean 4.',
			description:
				'Adds learned guidance to Lean 4 tactics like `grind` and `aesop`, combining neural branching heuristics with tooling for collecting and training on proof search data.',
			link: 'https://github.com/xvade/LeanHackathon2026',
			team: ['Theo Meek', 'Simon Chess', 'Evan Wang', 'Sophie Szeto'],
			highlight: 'purple',
			image: secondPlacePhoto,
			imageAlt: 'Second place winners posing with the Learned Tactic Branching project award'
		},
		{
			placement: '3rd Place',
			project: 'Lean Pool',
			tagline: 'A repository for Lean 4 formalizations outside mathlib’s scope.',
			description:
				'Collects Lean 4 formalizations outside mathlib’s scope, with a workflow for discovering projects, checking them automatically, and promoting accepted work into a shared library.',
			link: 'https://github.com/Vilin97/lean-pool',
			team: ['Vasily Ilin', 'Justin Asher'],
			highlight: 'silver',
			image: thirdPlacePhoto,
			imageAlt: 'Third place winners posing with the Lean Pool project award'
		}
	];

	const honorableMentions = [
		{
			project: 'LeanDream',
			link: 'https://github.com/ssingh92-ops/LeanDream',
			team: ['Nels Martin', 'Sukhman Singh', 'Tanish Vaidya']
		},
		{
			project: 'Zoogle',
			link: 'https://github.com/e-gubarev/zoogle',
			team: ['Evan Gubarev', 'Tim Avilov']
		},
		{
			project: 'Blossom',
			link: 'https://github.com/oe-parks/Blossom',
			team: ['Kieran Rullman', 'John Ye', 'Nicholas Mundy', 'Owen Parks']
		}
	];
</script>

<section id="projects" class="section" style="position: relative; overflow: hidden;">
	<div class="container">
		<h2 class="section-title">Winning Projects</h2>
		<p class="section-subtitle">
			The inaugural UW Lean Hackathon has concluded. These projects were recognized by the judges
			for their novelty, technical execution, and community impact!
		</p>

		<div class="winners-grid">
			{#each winningProjects as project, i}
				<article
					class="winner-card glass-card"
					class:winner-card-featured={project.highlight === 'gold'}
					class:winner-card-silver={project.highlight === 'silver'}
					style="animation-delay: {i * 0.08}s"
				>
					<div class="winner-image-wrap">
						<img src={project.image} alt={project.imageAlt} class="winner-image" />
					</div>

					<div class="winner-header">
						<span class="badge" class:badge-gold={project.highlight === 'gold'} class:badge-purple={project.highlight !== 'gold'}>
							{project.placement}
						</span>
						<a href={project.link} class="project-link" target="_blank" rel="noopener">View project ↗</a>
					</div>

					<h3>{project.project}</h3>
					<p class="winner-tagline">{project.tagline}</p>
					<p class="winner-description">{project.description}</p>

					<div class="team-block">
						<span class="team-label">Team</span>
						<p>{project.team.join(' • ')}</p>
					</div>
				</article>
			{/each}
		</div>

		<div class="honorable-mentions">
			<div class="honorable-header">
				<h3>Honorable Mentions</h3>
				<p>Recognized by the judges for standout work.</p>
			</div>

			<div class="mentions-grid">
				{#each honorableMentions as project, i}
					<article class="mention-card glass-card" style="animation-delay: {(i + winningProjects.length) * 0.06}s">
						<div class="mention-topline">
							<span class="mention-label">Honorable Mention</span>
							<a href={project.link} class="project-link" target="_blank" rel="noopener">View project ↗</a>
						</div>
						<h4>{project.project}</h4>
						<p>{project.team.join(' • ')}</p>
					</article>
				{/each}
			</div>
		</div>

		<div class="floating-snippet snippet-right">
			<pre><code><span class="kw">theorem</span> <span class="fn">winner_showcase</span> :
  first ∧ second ∧ third := by
  <span class="kw">repeat</span> constructor</code></pre>
		</div>
	</div>
</section>

<style>
	.winners-grid {
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 1.5rem;
		align-items: stretch;
	}

	.winner-card {
		position: relative;
		animation: fadeInUp 0.6s ease both;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		min-height: 100%;
	}

	.winner-card-featured {
		background: linear-gradient(135deg, rgba(232, 185, 49, 0.12), rgba(139, 84, 250, 0.1));
		border-color: rgba(232, 185, 49, 0.35);
		box-shadow: 0 20px 60px rgba(232, 185, 49, 0.08);
	}

	.winner-card-silver {
		background: linear-gradient(135deg, rgba(201, 170, 255, 0.08), rgba(255, 255, 255, 0.03));
	}

	.winner-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
		flex-wrap: wrap;
	}

	.winner-image-wrap {
		margin: -2rem -2rem 0;
		overflow: hidden;
		border-radius: 16px 16px 0 0;
		border-bottom: 1px solid rgba(139, 84, 250, 0.12);
	}

	.winner-image {
		display: block;
		width: 100%;
		height: 240px;
		object-fit: cover;
	}

	.project-link {
		font-size: 0.9rem;
		font-weight: 600;
	}

	.winner-card h3 {
		font-size: 1.6rem;
		line-height: 1.15;
	}

	.honorable-mentions {
		margin-top: 2.5rem;
		position: relative;
		z-index: 1;
	}

	.honorable-header {
		margin-bottom: 1.25rem;
	}

	.honorable-header h3 {
		font-size: 1.2rem;
		margin-bottom: 0.25rem;
	}

	.honorable-header p {
		color: var(--text-muted);
		font-size: 0.95rem;
	}

	.mentions-grid {
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 1rem;
	}

	.mention-card {
		padding: 1.25rem 1.35rem;
		animation: fadeInUp 0.6s ease both;
	}

	.mention-topline {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 0.75rem;
		margin-bottom: 0.75rem;
	}

	.mention-label {
		font-size: 0.72rem;
		font-weight: 700;
		letter-spacing: 0.06em;
		text-transform: uppercase;
		color: var(--purple-200);
	}

	.mention-card h4 {
		font-size: 1.1rem;
		margin-bottom: 0.45rem;
	}

	.mention-card p {
		color: var(--text-muted);
		font-size: 0.9rem;
		line-height: 1.6;
	}

	.winner-tagline {
		color: var(--gold-400);
		font-weight: 600;
	}

	.winner-description {
		color: var(--text-muted);
		font-size: 0.98rem;
		line-height: 1.7;
	}

	.team-block {
		margin-top: auto;
		padding-top: 1rem;
		border-top: 1px solid rgba(139, 84, 250, 0.12);
	}

	.team-label {
		display: block;
		font-size: 0.78rem;
		font-weight: 700;
		letter-spacing: 0.06em;
		text-transform: uppercase;
		color: var(--text-muted);
		margin-bottom: 0.4rem;
	}

	.team-block p {
		color: var(--text);
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

	.floating-snippet {
		position: absolute;
		background: rgba(20, 15, 35, 0.7);
		backdrop-filter: blur(16px);
		border: 1px solid rgba(139, 84, 250, 0.15);
		border-radius: 10px;
		padding: 1rem 1.25rem;
		font-family: var(--font-mono);
		font-size: 0.75rem;
		line-height: 1.5;
		color: var(--text);
		pointer-events: none;
		z-index: 0;
		opacity: 0.4;
	}

	.floating-snippet .kw { color: var(--purple-300); }
	.floating-snippet .fn { color: var(--gold-400); }

	.snippet-right {
		right: 2%;
		bottom: 4%;
		transform: rotate(1deg);
	}

	@media (max-width: 1024px) {
		.winners-grid {
			grid-template-columns: 1fr;
		}

		.mentions-grid {
			grid-template-columns: 1fr;
		}
	}

	@media (max-width: 768px) {
		.floating-snippet {
			display: none;
		}
	}
</style>
