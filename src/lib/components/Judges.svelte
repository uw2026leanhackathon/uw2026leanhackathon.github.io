<script lang="ts">
	interface PersonCard {
		name: string;
		affiliation?: string;
		note?: string;
		website?: string;
		accent: string;
	}

	interface GuestCard extends PersonCard {
		title: string;
		description: string;
	}

	const guests: GuestCard[] = [
		{
			name: 'Leo de Moura',
			affiliation: 'Amazon',
			title: 'Colloquium Speaker',
			description:
				'Creator of Lean. He spoke on machine-checked mathematics, AI collaboration, proof automation, and the role of Lean as long-term open infrastructure for verified software and mathematics.',
			website: 'https://leodemoura.github.io/',
			accent: '#f0cc5b'
		},
		{
			name: 'Eric Wieser',
			affiliation: 'Google DeepMind',
			title: 'Special Guest',
			description:
				'Supported teams throughout the event, drawing on his experience as a maintainer of mathlib and helping participants navigate formalization work in Lean.',
			accent: '#7cf0b5'
		}
	];

	const judges: PersonCard[] = [
		{ name: 'Varun Pant', affiliation: 'Amazon', accent: '#f0cc5b' },
		{ name: 'Eric Klavins', affiliation: 'ECE Department Chair', accent: '#7cf0b5' },
		{ name: 'Jarod Alper', affiliation: 'Math faculty and Google DeepMind', accent: '#a87cff' },
		{ name: 'Jesse Han', affiliation: 'Math Inc', website: 'https://jesse-michael-han.github.io/', accent: '#8b54fa' }
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
		<h2 class="section-title">Guests & Judges</h2>
		<p class="section-subtitle">
			Thanks to our special guests for sharing their expertise, and to our judges for helping make
			the inaugural UW Lean Hackathon possible.
		</p>

		<div class="guests-grid">
			{#each guests as guest, i}
				<article class="guest-card glass-card" style="animation-delay: {i * 0.08}s">
					<div class="guest-topline">
						<span class="guest-title">{guest.title}</span>
						{#if guest.website}
							<a href={guest.website} target="_blank" rel="noopener" class="guest-link">Website ↗</a>
						{/if}
					</div>

					<div class="guest-heading">
						<div class="guest-avatar" style="border-color: {guest.accent}">
							<span class="guest-initials" style="color: {guest.accent}">{getInitials(guest.name)}</span>
						</div>
						<div>
							<h3>{guest.name}</h3>
							{#if guest.affiliation}
								<span class="guest-affiliation" style="color: {guest.accent}">{guest.affiliation}</span>
							{/if}
						</div>
					</div>

					<p class="guest-description">{guest.description}</p>
				</article>
			{/each}
		</div>

		<div class="judges-block">
			<div class="judges-block-header">
				<h3>Judges</h3>
				<p>With thanks to the panel who evaluated projects and selected this year’s winners.</p>
			</div>

			<div class="judges-grid">
				{#each judges as judge, i}
					<article class="judge-card glass-card" style="animation-delay: {(i + guests.length) * 0.08}s">
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
						<h4>{judge.name}</h4>
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
	</div>
</section>

<style>
	.guests-grid {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: 1.5rem;
		margin-top: 2.5rem;
	}

	.guest-card {
		animation: fadeInUp 0.6s ease both;
		padding: 2rem;
	}

	.guest-topline {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
		margin-bottom: 1.25rem;
		flex-wrap: wrap;
	}

	.guest-title {
		font-size: 0.78rem;
		font-weight: 700;
		letter-spacing: 0.06em;
		text-transform: uppercase;
		color: var(--gold-400);
	}

	.guest-link {
		font-size: 0.9rem;
		font-weight: 600;
	}

	.guest-heading {
		display: flex;
		align-items: center;
		gap: 1rem;
		margin-bottom: 1rem;
	}

	.guest-avatar,
	.judge-avatar {
		width: 72px;
		height: 72px;
		border-radius: 50%;
		border: 2px solid;
		display: flex;
		align-items: center;
		justify-content: center;
		background: rgba(139, 84, 250, 0.08);
		transition: transform 0.2s ease, box-shadow 0.2s ease;
	}

	.guest-initials,
	.judge-initials {
		font-size: 1.35rem;
		font-weight: 700;
		font-family: var(--font-mono);
	}

	.guest-card h3 {
		font-size: 1.2rem;
		margin-bottom: 0.2rem;
	}

	.guest-affiliation,
	.judge-affiliation {
		font-size: 0.85rem;
		font-weight: 600;
	}

	.guest-description {
		color: var(--text-muted);
		font-size: 0.98rem;
		line-height: 1.7;
	}

	.judges-block {
		margin-top: 3rem;
	}

	.judges-block-header {
		margin-bottom: 1.25rem;
	}

	.judges-block-header h3 {
		font-size: 1.2rem;
		margin-bottom: 0.25rem;
	}

	.judges-block-header p {
		color: var(--text-muted);
		font-size: 0.95rem;
	}

	.judges-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
		gap: 1.25rem;
	}

	.judge-card {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		padding: 1.6rem 1.25rem;
		min-height: 220px;
		animation: fadeInUp 0.6s ease both;
	}

	.judge-avatar-link {
		display: inline-flex;
		border-radius: 50%;
		text-decoration: none;
		margin-bottom: 1rem;
	}

	.judge-avatar-link:hover .judge-avatar {
		transform: translateY(-2px);
		box-shadow: 0 12px 28px rgba(139, 84, 250, 0.16);
	}

	.judge-avatar {
		margin-bottom: 1rem;
	}

	.judge-card h4 {
		font-size: 1.02rem;
		color: var(--text-heading);
		margin-bottom: 0.35rem;
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

	@media (max-width: 900px) {
		.guests-grid {
			grid-template-columns: 1fr;
		}
	}
</style>
