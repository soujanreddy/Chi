<template lang="pug">
  <ComponentExample title="Vertical" :id="exampleId" additionalClasses="-bg--grey-20" padding="-p--0" :tabs="exampleTabs" :headTabs="headTabs" @chiHeadTabsChange="e => changeClosable(e)">
    .-p--3(slot="example")
      div(:class="'chi-grid -no-gutter -bg--' + (menuId === 'base' ? 'white' : 'black')")
        .chi-col.-w--6.-w-sm--4.-p--3
          ul(:class="'chi-tabs ' + (menuId === 'base' ? '' : '-inverse') + ' -vertical'" :id="'example-vertical-' + menuId" role="tablist" :aria-label="menuId === 'base' ? 'chi-tabs-vertical-base' : 'vertical-inverse'" :ref="menuId === 'base' ? 'example-vertical-base' : ''")
            li(:class="tab.id === 1 ? '-active' : ''" :key="tab.id" v-for="tab in $data.tabs")
              a(
                :href="'#vertical-' + menuId + '-' + tab.id"
                role="tab"
                :tabIndex="tab.id === 1 ? '' : '-1'"
                :aria-selected="tab.id === 1 ? 'true' : 'false'"
                :aria-controls="'vertical-' + menuId + '-' + tab.id") {{tab.label}}
        div(:class="'chi-col ' + (menuId === 'base' ? '' : '-bg--white') + ' -p--3'")
          div(:class="'chi-tabs-panel ' + (tab.id === 1 ? '-active' : '')" :id="'vertical-' + menuId + '-' + tab.id" :key="tab.id" v-for="tab in $data.tabs" role="tabpanel")
            .-text Tab {{tab.id}} content    
    <Wrapper :slot="`code-${exampleId}-${tab.id}-webcomponent`" v-for="tab in headTabs" :key="tab.id">
      <pre class="language-html">
        <code v-highlight="tab.codeSnippets.webComponent.code" class="html"></code>
      </pre>
    </Wrapper>
    <Wrapper :slot="`code-${exampleId}-${tab.id}-htmlblueprint`" v-for="tab in headTabs" :key="tab.id">
      <JSNeeded />
      <pre class="language-html">
        <code v-highlight="tab.codeSnippets.htmlBlueprint.code" class="html"></code>
      </pre>
    </Wrapper>
  </ComponentExample>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { HeadTabsInterface } from '../../../../models/models';

declare const chi: any;

@Component({
  data: () => {
    return {
      exampleId: 'vertical-lumen-centurylink',
      tabs: [{id: 1, label: 'Active Tab'}, {id: 2, label: 'Tab Link'}, {id: 3, label: 'Tab Link'}],
      exampleTabs: [
        {
          disabled: true,
          id: 'webcomponent',
          label: 'Web component',
        },
        {
          active: true,
          id: 'htmlblueprint',
          label: 'HTML blueprint',
        },
      ],
      headTabs: [
        {
          active: true,
          id: 'base',
          label: 'Base',
           codeSnippets: {
        webComponent: {
          code: ''
        },
        htmlBlueprint: {
          code: `<ul class="chi-tabs -vertical" id="example-vertical-base" role="tablist" aria-label="chi-tabs-vertical-base">
  <li class="-active">
    <a
      href="#vertical-base-1"
      role="tab"
      aria-selected="true"
      aria-controls="vertical-base-1">Active Tab</a>
  </li>
  <li>
    <a
      href="#vertical-base-2"
      role="tab"
      aria-selected="false"
      tabindex="-1"
      aria-controls="vertical-base-2">Tab Link</a>
  </li>
  <li>
    <a
      href="#vertical-base-3"
      role="tab"
      aria-selected="false"
      tabindex="-1"
      aria-controls="vertical-base-3">Tab Link</a>
  </li>
</ul>

<div class="chi-tabs-panel -active" id="vertical-base-1" role="tabpanel">
  Tab 1 content
</div>
<div class="chi-tabs-panel" id="vertical-base-2" role="tabpanel">
  Tab 2 content
</div>
<div class="chi-tabs-panel" id="vertical-base-3" role="tabpanel">
  Tab 3 content
</div>

<script>chi.tab(document.getElementById('example-vertical-base'));<\/script>`,
        }
        }
        },
        {
          id: 'inverse',
          label: 'Inverse',
          codeSnippets: {
        webComponent: {
          code: ''
        },
        htmlBlueprint: {
         code: `<ul class="chi-tabs -inverse -vertical" id="example-vertical-inverse" role="tablist" aria-label="vertical-inverse">
  <li class="-active">
    <a
      href="#vertical-inverse-1"
      role="tab"
      aria-selected="true"
      aria-controls="vertical-inverse-1">Active Tab</a>
  </li>
  <li>
    <a
      href="#vertical-inverse-2"
      role="tab"
      aria-selected="false"
      tabindex="-1"
      aria-controls="vertical-inverse-2">Tab Link</a>
  </li>
  <li>
    <a
      href="#vertical-inverse-3"
      role="tab"
      aria-selected="false"
      tabindex="-1"
      aria-controls="vertical-inverse-3">Tab Link</a>
  </li>
</ul>

<div class="chi-tabs-panel -active" id="vertical-inverse-1" role="tabpanel">
  Tab 1 content
</div>
<div class="chi-tabs-panel" id="vertical-inverse-2" role="tabpanel">
  Tab 2 content
</div>
<div class="chi-tabs-panel" id="vertical-inverse-3" role="tabpanel">
  Tab 3 content
</div>

<script>chi.tab(document.getElementById('example-vertical-inverse'));<\/script>`,
        },
      },
        },
      ],
    }
  },
})
export default class VerticalLumenCenturyLink extends Vue {
  menuId = 'base';
  tab: any;

  mounted() {
    this.tab = chi.tab(this.$refs['example-vertical-base'] as HTMLElement);
  }

  changeClosable(e: HeadTabsInterface) {
    this.menuId = e.id;
  }

  beforeDestroy() {
    this.tab.dispose();
  }
}
</script>
