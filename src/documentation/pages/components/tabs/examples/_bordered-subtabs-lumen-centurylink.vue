<template lang="pug">
  <ComponentExample title="Bordered" :id="exampleId" additionalClasses="-bg--grey-20" padding="-p--0" :tabs="exampleTabs" :headTabs="headTabs" @chiHeadTabsChange="e => changeClosable(e)">
    .-p--3(:class="menuId === 'base' ? '' : '-bg--grey-20'" slot="example")
      div(:class="menuId === 'base' ? '-bg--white' : '-bg--black'").-p--3
        ul.chi-tabs(:class="menuId === 'base' ? '' : '-inverse'").-border
          li.-active
            a(href='#') Active tab
          li
            a(href='#') Tab link
          li
            a(href='#') Tab link
    <Wrapper :slot="`code-${exampleId}-${tab.id}-webcomponent`" v-for="tab in headTabs" :key="tab.id">
      <pre class="language-html">
        <code v-highlight="tab.codeSnippets.webComponent.code" class="html"></code>
      </pre>
    </Wrapper>
    <Wrapper :slot="`code-${exampleId}-${tab.id}-htmlblueprint`" v-for="tab in headTabs" :key="tab.id">
      <pre class="language-html">
        <code v-highlight="tab.codeSnippets.htmlBlueprint.code" class="html"></code>
      </pre>
    </Wrapper>
  </ComponentExample>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { HeadTabsInterface } from '../../../../models/models';

@Component({
  data: () => {
    return {
      exampleId: 'bordered-portal',
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
              code: `<ul class="chi-tabs -border">
  <li class="-active">
    <a href="#">Active tab</a>
  </li>
  <li>
    <a href="#">Tab link</a>
  </li>
  <li>
    <a href="#">Tab link</a>
  </li>
</ul>`,
            }
          }
        },
        {
          id: 'inverse',
          label: 'Inverse',
          codeSnippets: {
            webComponent: ``,
            htmlBlueprint: {
              code: `<ul class="chi-tabs -inverse -border">
  <li class="-active">
    <a href="#">Active tab</a>
  </li>
  <li>
    <a href="#">Tab link</a>
  </li>
  <li>
    <a href="#">Tab link</a>
  </li>
</ul>`
            }
          }
        },
      ],
    };
  },
})
export default class BorderedSubtabsLumenCenturyLink extends Vue {
  menuId = 'base';

  changeClosable(e: HeadTabsInterface) {
    this.menuId = e.id;
  }
}
</script>