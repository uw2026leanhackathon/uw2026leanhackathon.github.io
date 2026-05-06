<script lang="ts">
	interface Judge {
		name: string;
		affiliation?: string;
		note?: string;
		website?: string;
		accent: string;
	}

	const judges: Judge[] = [
		{ name: 'Varun Pant', affiliation: 'Amazon', accent: '#f0cc5b' },
		{ name: 'Eric Klavins', affiliation: 'ECE Department Chair', accent: '#7cf0b5' },
		{ name: 'Jarod Alper', affiliation: 'Math faculty and Google DeepMind', accent: '#a87cff' },
	];

	function getInitials(name: string): string {
		return name
			.split(' ')
			.map((part) => part[0])
			.join('');
	}
</script>

<section id="judges" class="section">
	<div class="container">
		<h2 class="section-title">Judges</h2>

		<div class="judges-grid">
			{#each judges as judge, i}
				<article class="judge-card glass-card" style="animation-delay: {i * 0.08}s">
					{#if judge.website}
						<a
							href={judge.website}
							target="_blank"
							rel="noopener"
							class="judge-avatar-link"
							aria-label="Visit {judge.name}'s website"
						>
							<div class="judge-avatar" style="border-color: {judge.accent}">
								<span class="judge-initials" style="color: {judge.accent}">{getInitials(judge.name)}</span>
							</div>
						</a>
					{:else}
						<div class="judge-avatar" style="border-color: {judge.accent}">
							<span class="judge-initials" style="color: {judge.accent}">{getInitials(judge.name)}</span>
						</div>
					{/if}
					<h3>{judge.name}</h3>
					{#if judge.affiliation}
						<span class="judge-affiliation" style="color: {judge.accent}">{judge.affiliation}</span>
					{/if}
					{#if judge.note}
						<span class="judge-note">{judge.note}</span>
					{/if}
				</article>
			{/each}
		</div>
	</div>
</section>

<style>
	.judges-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
		gap: 1.25rem;
		margin-top: 2.5rem;
	}

	.judge-card {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		padding: 2rem 1.5rem;
		min-height: 240px;
		animation: fadeInUp 0.6s ease both;
	}

	.judge-avatar-link {
		display: inline-flex;
		border-radius: 50%;
		text-decoration: none;
	}

	.judge-avatar-link:hover .judge-avatar {
		transform: translateY(-2px);
		box-shadow: 0 12px 28px rgba(139, 84, 250, 0.16);
	}

	.judge-avatar {
		width: 72px;
		height: 72px;
		border-radius: 50%;
		border: 2px solid;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 1rem;
		background: rgba(139, 84, 250, 0.08);
		transition: transform 0.2s ease, box-shadow 0.2s ease;
	}

	.judge-initials {
		font-size: 1.35rem;
		font-weight: 700;
		font-family: var(--font-mono);
	}

	.judge-card h3 {
		font-size: 1.05rem;
		color: var(--text-heading);
		margin-bottom: 0.35rem;
	}

	.judge-affiliation {
		font-size: 0.85rem;
		font-weight: 600;
	}

	.judge-note {
		margin-top: 0.75rem;
		padding: 0.3rem 0.7rem;
		border-radius: 999px;
		border: 1px solid rgba(240, 204, 91, 0.3);
		background: rgba(240, 204, 91, 0.08);
		color: var(--gold-400);
		font-size: 0.75rem;
		font-weight: 600;
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
</style>
