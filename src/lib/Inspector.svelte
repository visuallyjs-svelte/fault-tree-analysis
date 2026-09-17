<script>
    import { Node } from "@visuallyjs/browser-ui"
    import { InspectorComponent } from "@visuallyjs/browser-ui-svelte";

    let current = $state(null)
</script>

<InspectorComponent bind:current={current}>
    {#if current != null}
        <div class="vjs-fta-inspector-container">
            {#if current.objectType === Node.objectType}
                <div class="vjs-fta-inspector-group">
                    <label class="vjs-fta-inspector-label">Label: </label>
                    <input 
                        type="text" 
                        class="vjs-fta-inspector-input"
                        vjs-att="label"
                        vjs-focus="true"
                    />
                </div>
                
                {#if current.type === 'basic-event'}
                    <div class="vjs-fta-inspector-group">
                        <label class="vjs-fta-inspector-label">Probability (0-1): </label>
                        <input 
                            type="number" 
                            class="vjs-fta-inspector-input"
                            step="0.01" 
                            min="0" 
                            max="1" 
                            vjs-att="probability"
                            vjs-datatype="float"
                        />
                    </div>
                {/if}
                
                <div class="vjs-fta-inspector-footer">
                    ID: {current.getFullId()}<br/>
                    Type: {current.type}
                </div>
            {:else}
                <div class="vjs-fta-inspector-footer">
                    ID: {current.getFullId()}<br/>
                    Type: {current.objectType}
                </div>
            {/if}
        </div>
    {:else}
        <div class="vjs-fta-inspector-empty">Select a node to edit its properties.</div>
    {/if}
</InspectorComponent>
