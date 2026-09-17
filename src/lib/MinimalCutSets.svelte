<script>
    import { useVisuallyJsUpdate } from "@visuallyjs/browser-ui-svelte";
    import { computeCutSets } from "../cut-sets";

    let minimalCutSets = $state([]);

    useVisuallyJsUpdate((model) => {
        minimalCutSets = computeCutSets(model);
    })
</script>

<div class="minimal-cut-sets">
    {#if minimalCutSets.length === 0}
        <p class="vjs-fta-inspector-empty">No cut sets found.</p>
    {:else}
        <div class="vjs-fta-cut-sets-list">
            {#each minimalCutSets as set, i}
                <div class="vjs-fta-cut-set">
                    <div class="vjs-fta-cut-set-index">#{i + 1}</div>
                    <div class="vjs-fta-cut-set-events">
                        {#each set as be (be.id)}
                            <span class="vjs-fta-cut-set-event">
                                {be.label || be.id}
                            </span>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>
    {/if}
    <p class="vjs-fta-cut-sets-note"><i>Note: This is a static, combinatorial analysis. It does not account for event sequence or timing.</i></p>
</div>
