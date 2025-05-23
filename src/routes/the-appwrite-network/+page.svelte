<script lang="ts">
    import Map from '$lib/components/appwrite-network/map.svelte';
    import { InlineTag, Icon } from '$lib/components/ui';
    import GradientText from '$lib/components/ui/gradient-text.svelte';
    import { Main } from '$lib/layouts';
    import { classNames } from '$lib/utils/classnames';
    import {
        DEFAULT_DESCRIPTION,
        DEFAULT_HOST,
        getInlinedScriptTag,
        organizationJsonSchema,
        softwareAppSchema
    } from '$lib/utils/metadata';

    const title = 'The Appwrite Network';
    const description = DEFAULT_DESCRIPTION;
    const ogImage = `${DEFAULT_HOST}/images/open-graph/website.png`;

    const heading = 'The Appwrite Network';
</script>

<svelte:head>
    <!-- Titles -->
    <title>{title}</title>
    <meta property="og:title" content={title} />
    <meta name="twitter:title" content={title} />
    <!-- Description -->
    <meta name="description" content={description} />
    <meta property="og:description" content={description} />
    <meta name="twitter:description" content={description} />
    <!-- Image -->
    <meta property="og:image" content={ogImage} />
    <meta property="og:image:width" content="1200" />
    <meta property="og:image:height" content="630" />
    <meta name="twitter:image" content={ogImage} />
    <meta name="twitter:card" content="summary_large_image" />

    <!-- eslint-disable-next-line svelte/no-at-html-tags-->
    {@html getInlinedScriptTag(softwareAppSchema())}

    <!-- eslint-disable-next-line svelte/no-at-html-tags-->
    {@html getInlinedScriptTag(organizationJsonSchema())}
</svelte:head>

<Main>
    <div class="relative max-w-screen overflow-hidden">
        <div class="container mt-20 flex flex-col items-center">
            <a
                href="/blog/post/the-appwrite-network"
                class="bg-accent/4 animate-enter group border-accent/36 text-primary relative -mb-8 flex items-center gap-2 rounded-full border px-4 py-1 text-sm"
                style:animation-delay="250ms"
                >Read the announcement <Icon
                    name="arrow-right"
                    class="transition group-hover:translate-x-0.5"
                /></a
            >
            <h1 class="text-display font-aeonik-pro mx-auto inline-block py-12 text-center">
                {#each heading.split(' ') as word, i}
                    <GradientText
                        class="animate-enter mr-2 inline-block"
                        style="animation-delay:{i * 75}ms">{word}</GradientText
                    >
                {/each}
            </h1>
        </div>

        <div
            class={classNames(
                'animate-lighting absolute top-0 left-0 -z-10 h-screen w-[200vw] -translate-x-[25%] translate-y-8 rotate-25 overflow-hidden blur-3xl md:w-full',
                'bg-[image:radial-gradient(ellipse_390px_50px_at_10%_30%,_rgba(254,_149,_103,_0.2)_0%,_rgba(254,_149,_103,_0)_70%),_radial-gradient(ellipse_1100px_170px_at_15%_40%,rgba(253,_54,_110,_0.08)_0%,_rgba(253,_54,_110,_0)_70%),_radial-gradient(ellipse_1200px_180px_at_30%_30%,_rgba(253,_54,_110,_0.08)_0%,_rgba(253,_54,_110,_0)_70%)]',
                'bg-position-[0%_0%]'
            )}
        ></div>
        <div class="mb-20">
            <Map />
        </div>
    </div>
</Main>
