<script lang="ts">
	const challenges = [
		{
			title: 'Proof by Algorithm: Linear Programming',
			description: 'Write a tactic that can prove a given point is an optimal solution to a linear program (using duality).'
		},
		{
			title: 'Proof by Algorithm: Graph Algorithms',
			description: 'Implement algorithms for graphs such as computing augmenting paths for matchings and flows. Prove that these paths really do augment the matching/flow in the appropriate way.'
		},
		{
			title: 'Proof by Picture: Paper Folding',
			description: 'Formalize the Huzita–Hatori Axioms of Paper Folding in Lean and prove that they can be used to solve cubic equations. Build a tool to visualize the folds and verifiably compute the coordinates of points obtained through folds.'
		},
		{
			title: 'Sudoku in Lean',
			description: 'Make Sudoku in Lean. Write a solver for Sudoku in Lean. Prove the correctness of your solver.'
		},
		{
			title: 'Data Structures for Lean',
			description: 'Port a useful data structure to Lean and write useful theorems about it. For example, there are many variants of map data structures which may be useful. See <a href="https://github.com/bendyworks/lean-map" target="_blank" rel="noopener">lean-map</a> for inspiration.'
		}
	];
</script>

<section id="projects" class="section" style="position: relative; overflow: hidden;">
	<div class="container">
		<h2 class="section-title">Project Ideas</h2>
		<p class="section-subtitle">
			Use these project ideas as inspiration. Feel free to pick from this list, but make sure to put in your own twist! Up-to-date as of April 1, 2026.
		</p>

		<ul class="challenges-list">
			{#each challenges as challenge, i}
				<li class="challenge-item" style="animation-delay: {i * 0.06}s">
					<span class="challenge-marker"></span>
					<div class="challenge-content">
						<h3>{challenge.title}</h3>
						<p>{@html challenge.description}</p>
					</div>
				</li>
			{/each}
		</ul>

		<!-- Decorative Lean snippets -->
		<div class="floating-snippet snippet-left">
			<pre><code><span class="kw">theorem</span> <span class="fn">inf_primes</span> (n : ℕ) :
    ∃ p, n ≤ p ∧ Nat.Prime p :=
  <span class="fn">Nat.exists_infinite_primes</span> n</code></pre>
		</div>
		<div class="floating-snippet snippet-right">
			<pre><code><span class="kw">#check</span> @List.map
<span class="cm">-- {'{'}&alpha; &beta; : Type{'}'} &rarr;</span>
<span class="cm">--   (&alpha; &rarr; &beta;) &rarr; List &alpha; &rarr; List &beta;</span></code></pre>
		</div>
	</div>
</section>

<style>
	.challenges-list {
		list-style: none;
		max-width: 800px;
		margin: 0 auto;
	}

	.challenge-item {
		display: flex;
		align-items: flex-start;
		gap: 1.25rem;
		padding: 1.25rem 0;
		border-bottom: 1px solid rgba(139, 84, 250, 0.08);
		animation: fadeInUp 0.5s ease both;
	}

	.challenge-item:last-child {
		border-bottom: none;
	}

	.challenge-marker {
		flex-shrink: 0;
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: var(--purple-400);
		margin-top: 0.55rem;
	}

	.challenge-content h3 {
		font-size: 1.1rem;
		color: var(--text-heading);
		margin-bottom: 0.3rem;
	}

	.challenge-content p {
		color: var(--text-muted);
		font-size: 0.95rem;
		line-height: 1.6;
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

	@media (max-width: 768px) {
		.challenges-list {
			max-width: 100%;
		}
		.floating-snippet {
			display: none;
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
	.floating-snippet .cm { color: var(--text-muted); }

	.snippet-left {
		left: 2%;
		bottom: 6%;
		transform: rotate(-1.5deg);
	}

	.snippet-right {
		right: 2%;
		top: 8%;
		transform: rotate(1deg);
	}
</style>
