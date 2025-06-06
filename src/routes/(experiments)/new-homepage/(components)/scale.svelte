<script lang="ts">
    import { classNames } from '$lib/utils/classnames';
    import NumberFlow from '@number-flow/svelte';
    import { inView } from 'motion-legacy';
    import { onDestroy } from 'svelte';
    import KCollectTestimonialImage from '../../../products/sites/kcollect-ryan-testimonial.png';

    const animationDuration = 3;

    let stats = [
        {
            number: 0,
            suffix: '+',
            description: 'Regions served',
            top: 93.75
        },
        {
            number: 0,
            suffix: '+ TB',
            description: 'of data served',
            top: 78.25
        },
        {
            number: 0,
            suffix: 'B',
            description: 'requests',
            top: 62.5
        },
        {
            number: 0,
            suffix: 'K',
            description: 'projects',
            top: 46.75
        }
    ];

    let alternateStats = [
        {
            number: 0,
            suffix: 'K+',
            description: 'Github stars',
            top: 93.75
        },
        {
            number: 0,
            suffix: '+',
            description: 'PoP locations',
            top: 78.25
        },
        {
            number: 0,
            suffix: 'K+',
            description: 'developers',
            top: 62.5
        },
        {
            number: 0,
            suffix: 'B+',
            description: 'monthly database operations',
            top: 46.75
        }
    ];

    const numbers = [12, 1000, 50, 300];
    const alternateNumbers = [50, 300, 300, 20];

    let animate: boolean = false;

    let timeoutIds: Array<NodeJS.Timeout> = [];
    const updateNumbers = () => {
        correctStats.forEach((stat, index) => {
            const timeoutId = setTimeout(
                () => {
                    correctStats[index] = { ...stat, number: correctNumbers[index] };
                },
                ((index * animationDuration) / correctNumbers.length) * 500
            );

            timeoutIds.push(timeoutId);
        });
    };

    const useInView = (node: HTMLElement) => {
        inView(
            node,
            () => {
                animate = true;
                updateNumbers();
            },
            { amount: 0.5 }
        );
    };

    const clearAllTimeouts = () => {
        timeoutIds.forEach((timeoutId) => {
            clearTimeout(timeoutId);
        });

        timeoutIds = [];
    };

    onDestroy(() => {
        clearAllTimeouts();
    });

    export let theme: 'light' | 'dark' = 'dark';
    export let alternateInfo: boolean = false;

    const correctStats = alternateInfo ? alternateStats : stats;
    const correctNumbers = alternateInfo ? alternateNumbers : numbers;
    const testimonial = {
        name: 'Ryan O’Conner',
        copy: `The switch to using Appwrite brought infinite value that I'm still discovering today, but a major impact that it made was the amount of time and stress that it saved me as it simply just works.`,
        image: KCollectTestimonialImage,
        title: 'Founder',
        company: 'K-Collect'
    };

    const getCorrectText = () => {
        if (!alternateInfo) {
            return {
                partOne: 'Appwrite has supported our recent growth in every step of the way,',
                partTwo: 'without any failures or outages.'
            };
        } else {
            return {
                partOne: 'The switch to using Appwrite brought',
                partTwo: "infinite value that I'm still discovering today."
            };
        }
    };

    const text = getCorrectText();
</script>

<div
    class={classNames(
        'relative flex min-h-[70vh] flex-col gap-4',
        theme === 'dark' ? 'border-smooth border-y bg-black/8 py-20' : ''
    )}
    use:useInView
>
    <div class="relative z-10 container w-fit md:w-full">
        <div class="max-w-xl">
            <h2 class="text-primary font-aeonik-pro text-5xl tracking-tighter text-pretty">
                Thousands of developers <span class="text-secondary">scale with Appwrite</span><span
                    class="text-accent">_</span
                >
            </h2>
            <p class="text-secondary border-accent mt-5 border-l-2 pr-28 pl-2 font-medium">
                <span class="text-accent">“</span>{text.partOne}
                <span class="text-primary">{text.partTwo}</span><span class="text-accent">”</span>
            </p>

            {#if alternateInfo}
                <div class="mt-4 flex items-center gap-3">
                    <img
                        src={testimonial.image}
                        class="size-6 rounded-full"
                        alt="{testimonial.company} Logo"
                    />
                    <div class="flex gap-1">
                        <span class="text-primary text-sub-body block font-medium">
                            {testimonial.name},
                        </span>
                        <span class="text-sub-body text-secondary block"
                            >{testimonial.title} at {testimonial.company}</span
                        >
                    </div>
                </div>
            {/if}
        </div>
    </div>

    <div class="mt-12 block space-y-8 md:hidden">
        {#each correctStats as stat, i}
            <div class="h-full overflow-auto pl-6">
                <div class={classNames('relative')} style:top={`${(4 - i) * 18}%`}>
                    <NumberFlow
                        class="text-description text-primary border-accent relative -left-px z-10 border-l pl-4 font-medium"
                        value={stat.number}
                        suffix={stat.suffix}
                    />
                    <span class="text-body text-secondary block pl-4">{stat.description}</span>
                </div>
            </div>
        {/each}
    </div>

    <div
        class="swipe mask absolute inset-0 hidden md:block"
        style:--animation-duration={`${animationDuration}s`}
        style:--mask-height="50px"
    >
        <div class="relative container h-full">
            <div class="absolute inset-0 z-100 grid grid-cols-4">
                {#each correctStats as stat, i}
                    <div
                        class="mask border-smooth h-full overflow-auto border-l"
                        style:--mask-direction="bottom"
                        style:--mask-height={`${(4 - i) * 25}%`}
                    >
                        <div class={classNames('relative')} style:top={`${(4 - i) * 18}%`}>
                            <NumberFlow
                                class="text-description text-primary border-accent relative -left-px z-10 border-l pl-4 font-medium"
                                value={stat.number}
                                suffix={stat.suffix}
                            />
                            <span class="text-body text-secondary block pl-4"
                                >{stat.description}</span
                            >
                        </div>
                    </div>
                {/each}

                <!-- <div class="pointer-events-none absolute inset-0 z-50">
                    {#each correctStats as stat, i}
                        <div
                            class="border-accent absolute top-[var(--top)] left-[calc(var(--left)_+_1px)] h-2 w-2 -translate-1/2 rounded-full border bg-white"
                            style:--top={`${stat.top}%`}
                            style:--left="{i * 25}%"
                        ></div>
                    {/each}
                </div> -->
            </div>
        </div>
        <div
            class="from-accent/15 absolute inset-0 bg-gradient-to-tr to-transparent [clip-path:polygon(0_100%,_100%_25%,_100%_100%,_0_100%)]"
        ></div>
        <div
            class="from-accent absolute inset-0 bg-gradient-to-r to-transparent [clip-path:polygon(0_100%,_100%_25%,_100%_25.1%,_0_100.1%)]"
        ></div>
    </div>
</div>

<style>
    .swipe {
        animation: wipe-in var(--animation-duration) ease-in-out;
    }

    @keyframes mask-wipe {
        0% {
            transform: translateX(0);
        }
        100% {
            transform: translateX(100%);
        }
    }

    @keyframes wipe-in {
        0% {
            clip-path: polygon(0% 0%, 0% 0%, 0% 100%, 0% 100%);
        }
        100% {
            clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
        }
    }
</style>
