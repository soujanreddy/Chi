<template lang="pug">
  <ComponentExample title="Vertical Subtabs" :id="exampleId" additionalClasses="-bg--grey-20" padding="-p--0" :tabs="exampleTabs" :headTabs="headTabs" @chiHeadTabsChange="e => changeClosable(e)">
    .-p--3(slot="example")
      div(:class="`-bg--${menuId === 'base' ? 'white' : 'black'} -p--3`")
        ul(:class="`chi-tabs ${menuId === 'base' ? '' : '-inverse'} -vertical`")
          li(:class="index === 0 ? '-active' : ''" v-for="(tab, index) in ['Active Tab', 'Tab Link', 'Tab Link']")
            a(href='#') {{tab}}
            ul.chi-tabs__subtabs(v-if="index === 0")
              li(:class="subTabindex === 0 ? '-active' : ''" v-for="(subTab, subTabindex) in ['Subtab Link', 'Subtab Link', 'Subtab Link']")
                a(href='#') {{subTab}}
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
      exampleId: 'vertical-subtabs-lumen-centurylink',
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
          code: `<ul class="chi-tabs -vertical">
  <li class="-active">
    <a href="#">Active tab</a>
    <ul class="chi-tabs__subtabs">
      <li class="-active">
        <a href="#">Subtab Link</a>
      </li>
      <li>
        <a href="#">Subtab Link</a>
      </li>
      <li>
        <a href="#">Subtab Link</a>
      </li>
    </ul>
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
        webComponent: {
          code: ''
        },
        htmlBlueprint: {
          code: `<ul class="chi-tabs -inverse -vertical">
  <li class="-active">
    <a href="#">Active tab</a>
    <ul class="chi-tabs__subtabs">
      <li class="-active">
        <a href="#">Subtab Link</a>
      </li>
      <li>
        <a href="#">Subtab Link</a>
      </li>
      <li>
        <a href="#">Subtab Link</a>
      </li>
    </ul>
  </li>
  <li>
    <a href="#">Tab link</a>
  </li>
  <li>
    <a href="#">Tab link</a>
  </li>
</ul>`
        },
      },
        },
      ],
     
    };
  },
})
export default class VerticalSubtabsLumenCenturyLink extends Vue {
  menuId = 'base';

  changeClosable(e: HeadTabsInterface) {
    this.menuId = e.id;
  }
}
</script>
