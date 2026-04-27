<script lang="ts">
	interface ScheduleEvent {
		time: string;
		title: string;
		speaker?: string;
		speakerUrl?: string;
		description?: string;
		abstract?: string;
		venue: string;
		type: 'talk' | 'hack' | 'food' | 'social' | 'ceremony';
	}

	interface ScheduleDay {
		date: string;
		label: string;
		events: ScheduleEvent[];
	}

	const schedule: ScheduleDay[] = [
		{
			date: 'May 1 (Fri)',
			label: 'Team Initial Meetup',
			events: [
				{
					time: '3:30 – 5:30 PM',
					title: 'Team Initial Meetup',
					description: 'Meet your team and get setup with Lean.',
					venue: 'ECE 269',
					type: 'social'
				}
			]
		},
		{
			date: 'May 8 (Fri)',
			label: 'Colloquium & Reception',
			events: [
				{
					time: '3:30 – 4:30 PM',
					title: 'Lean: Machine-Checked Mathematics and AI Collaboration',
					speaker: 'Leonardo de Moura',
					speakerUrl: 'https://leodemoura.github.io/',
					description:
						'Leonardo de Moura is a Senior Principal Applied Scientist in the Automated Reasoning Group at AWS. He is also the Chief Architect and co-founder of the Lean FRO, a non-profit organization dedicated to the development of the Lean theorem prover and programming language.',
					abstract: [
						'Lean is a proof assistant and programming language designed to make formal verification practical. In this talk, I will describe how Lean works, what it can do today, and where it is going.',
						'The core idea is simple: every mathematical claim and every program can be checked by a machine. This changes what collaboration looks like: between mathematicians, between engineers, and increasingly between humans and AI systems. When a proof is machine-checked, you do not need to trust the author. You just check it.',
						'I will discuss recent work on proof automation and AI-assisted formalization, including experiments where multi-agent AI systems work autonomously on Lean tasks. I will also describe the Lean FRO, a nonprofit building Lean as long-term open infrastructure for mathematics and verified software.'
					].join('\n\n'),
					venue: 'ECE 105',
					type: 'talk'
				},
				{
					time: '4:30 – 6:00 PM',
					title: 'Reception',
					description: 'Reception for hackathon participants along with faculty from Mathematics, Computer Science, and ECE.',
					venue: 'ECE 269',
					type: 'social'
				}
			]
		},
		{
			date: 'May 9 (Sat)',
			label: 'Hacking Day 1',
			events: [
				{ time: '9:00 AM', title: 'Registration & Coffee', venue: 'ECE 2nd Floor Atrium', type: 'food' },
				{ time: '10:00 – 10:30 AM', title: 'Event Kickoff', venue: 'ECE 269', type: 'talk' },
				{ time: '10:30 AM – 12:00 PM', title: 'Hacking Session 1', venue: 'ECE 269, ECE 303, ECE 403', type: 'hack' },
				{ time: '12:00 – 1:30 PM', title: 'Lunch', venue: 'ECE 2nd Floor Atrium', type: 'food' },
				{ time: '1:30 – 5:30 PM', title: 'Hacking Session 2', venue: 'ECE 269, ECE 303, ECE 403', type: 'hack' },
				{ time: '5:30 PM', title: 'Dinner', venue: 'ECE 2nd Floor Atrium', type: 'food' },
				{ time: 'until 9:00 PM', title: 'Hacking Session 3', venue: 'ECE 269, ECE 303, ECE 403', type: 'hack' }
			]
		},
		{
			date: 'May 10 (Sun)',
			label: 'Hacking Day 2',
			events: [
				{ time: '9:00 AM', title: 'Coffee', venue: 'ECE 2nd Floor Atrium', type: 'food' },
				{ time: '9:30 AM – 12:00 PM', title: 'Hacking Session 4', venue: 'ECE 269, ECE 303, ECE 403', type: 'hack' },
				{ time: '12:00 – 1:00 PM', title: 'Lunch', venue: 'ECE 2nd Floor Atrium', type: 'food' },
				{ time: '1:00 – 2:00 PM', title: 'Hacking Session 5', venue: 'ECE 269, ECE 303, ECE 403', type: 'hack' },
				{ time: '2:00 – 3:30 PM', title: 'Project Wrap-up ➕ Judging', venue: 'ECE 269, ECE 303, ECE 403', type: 'hack' },
				{ time: '4:00 PM', title: 'Event Close ➕ Awards and Prizes', venue: 'ECE 269', type: 'ceremony' }
			]
		}
	];

	let activeDay = $state(2);

	const typeColors: Record<string, string> = {
		talk: '#a87cff',
		hack: '#8b54fa',
		food: '#f0cc5b',
		social: '#c9aaff',
		ceremony: '#e8b931'
	};

	const typeLabels: Record<string, string> = {
		talk: '🎤 Talk',
		hack: '💻 Hack',
		food: '🍕 Food',
		social: '🤝 Social',
		ceremony: '🏆 Ceremony'
	};
</script>

<section id="schedule" class="section">
	<div class="container">
		<h2 class="section-title">Schedule</h2>

		<div class="day-tabs">
			{#each schedule as day, i}
				<button
					class="day-tab"
					class:active={activeDay === i}
					onclick={() => (activeDay = i)}
				>
					<span class="day-tab-date">{day.date}</span>
					<span class="day-tab-label">{day.label}</span>
				</button>
			{/each}
		</div>

		{#key activeDay}
			<div class="timeline">
				{#each schedule[activeDay].events as event, i}
					<div class="timeline-item" style="animation-delay: {i * 0.08}s">
						<div class="timeline-marker" style="background: {typeColors[event.type]}"></div>
						<div class="timeline-content glass-card">
							<div class="timeline-header">
								<span class="timeline-time">{event.time}</span>
								<span class="timeline-type" style="color: {typeColors[event.type]}">{typeLabels[event.type]}</span>
							</div>
							<h3>{event.title}</h3>
						{#if event.speaker}
							<p class="timeline-speaker">
								{#if event.speakerUrl}
									<a href={event.speakerUrl} target="_blank" rel="noopener">{event.speaker}</a>
								{:else}
									{event.speaker}
								{/if}
							</p>
						{/if}
						<div class="timeline-venue-badge" aria-label="Event location">
							<span class="timeline-venue-icon">📍</span>
							<span>{event.venue}</span>
						</div>
						{#if event.description}
							<p>{event.description}</p>
						{/if}
						{#if event.abstract}
							<div class="timeline-abstract">
								<span class="abstract-label">Abstract</span>
								<p>{event.abstract}</p>
							</div>
							{/if}
						</div>
					</div>
				{/each}
			</div>
		{/key}
	</div>
</section>

<style>
	.day-tabs {
		display: flex;
		gap: 0.75rem;
		margin-bottom: 3rem;
		flex-wrap: wrap;
	}

	.day-tab {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		padding: 1rem 1.5rem;
		border-radius: 12px;
		border: 1px solid rgba(139, 84, 250, 0.15);
		background: rgba(30, 22, 50, 0.5);
		cursor: pointer;
		transition: all 0.3s ease;
		color: var(--text-muted);
		min-width: 160px;
	}

	.day-tab:hover {
		border-color: rgba(139, 84, 250, 0.4);
		background: rgba(139, 84, 250, 0.08);
	}

	.day-tab.active {
		border-color: var(--purple-400);
		background: rgba(139, 84, 250, 0.15);
		color: white;
		box-shadow: 0 4px 20px rgba(139, 84, 250, 0.2);
	}

	.day-tab-date {
		font-size: 0.8rem;
		font-weight: 600;
		opacity: 0.8;
	}

	.day-tab-label {
		font-size: 1rem;
		font-weight: 700;
	}

	.timeline {
		position: relative;
		padding-left: 2rem;
	}

	.timeline::before {
		content: '';
		position: absolute;
		left: 6px;
		top: 0;
		bottom: 0;
		width: 2px;
		background: linear-gradient(to bottom, var(--purple-400), transparent);
	}

	.timeline-item {
		position: relative;
		margin-bottom: 1.25rem;
		animation: fadeInLeft 0.5s ease both;
	}

	.timeline-marker {
		position: absolute;
		left: -2rem;
		top: 1.5rem;
		width: 14px;
		height: 14px;
		border-radius: 50%;
		transform: translateX(-3px);
		box-shadow: 0 0 12px rgba(139, 84, 250, 0.4);
	}

	.timeline-content {
		padding: 1.25rem 1.5rem;
	}

	.timeline-content:hover {
		transform: translateY(-2px);
	}

	.timeline-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 0.5rem;
		flex-wrap: wrap;
		gap: 0.5rem;
	}

	.timeline-time {
		font-family: var(--font-mono);
		font-size: 0.85rem;
		color: var(--purple-300);
		font-weight: 500;
	}

	.timeline-type {
		font-size: 0.75rem;
		font-weight: 600;
	}

	.timeline-content h3 {
		font-size: 1.1rem;
		color: var(--text-heading);
		margin-bottom: 0.3rem;
	}

	.timeline-venue-badge {
		display: inline-flex;
		align-items: center;
		gap: 0.45rem;
		padding: 0.45rem 0.8rem;
		margin-bottom: 0.75rem;
		border-radius: 999px;
		border: 1px solid rgba(139, 84, 250, 0.28);
		background: rgba(139, 84, 250, 0.12);
		color: var(--text-heading);
		font-size: 0.8rem;
		font-weight: 600;
		letter-spacing: 0.01em;
	}

	.timeline-venue-icon {
		font-size: 0.85rem;
		line-height: 1;
	}

	.timeline-content p {
		color: var(--text-muted);
		font-size: 0.9rem;
		line-height: 1.5;
	}

	.timeline-speaker {
		font-size: 0.9rem;
		color: var(--gold-400);
		font-weight: 500;
		margin-bottom: 0.3rem;
	}

	.timeline-speaker a {
		color: inherit;
		text-decoration: underline;
		text-decoration-color: rgba(240, 204, 91, 0.45);
		text-underline-offset: 0.16em;
	}

	.timeline-speaker a:hover {
		text-decoration-color: currentColor;
	}

	.timeline-abstract {
		margin-top: 0.75rem;
		padding-top: 0.75rem;
		border-top: 1px solid rgba(139, 84, 250, 0.1);
	}

	.abstract-label {
		display: inline-block;
		font-size: 0.7rem;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		color: var(--purple-300);
		margin-bottom: 0.4rem;
	}

	.timeline-abstract p {
		font-size: 0.85rem;
		line-height: 1.6;
		color: var(--text-muted);
		opacity: 0.85;
		white-space: pre-line;
	}

	@keyframes fadeInLeft {
		from {
			opacity: 0;
			transform: translateX(-20px);
		}
		to {
			opacity: 1;
			transform: translateX(0);
		}
	}

	@media (max-width: 768px) {
		.day-tabs {
			gap: 0.5rem;
		}
		.day-tab {
			min-width: auto;
			padding: 0.75rem 1rem;
		}
	}
</style>
