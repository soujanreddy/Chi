<template lang="pug">
  <ComponentExample title="Vertical tabs with icons" :id="exampleId" additionalClasses="-bg--grey-20" padding="-p--0" :tabs="exampleTabs" :headTabs="headTabs" @chiHeadTabsChange="e => changeClosable(e)">
    .-p--3(slot="example")
      div(:class="`-bg--${menuId === 'base' ? 'white' : 'black'} -p--3`")
        ul(:class="`chi-tabs ${menuId === 'base' ? '' : '-inverse'} -vertical -icons`")
          li(:class="index === 0 ? '-active' : ''" v-for="(tab, index) in ['Active Tab', 'Tab Link', 'Tab Link']")
            a(href='#')
              i.chi-icon.icon-atom(aria-hidden="true")
              span {{tab}}
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
      exampleId: 'icons-vertical-lumen-centurylink',
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
          code: `<ul class="chi-tabs -vertical -icons">
  <li class="-active">
    <a href="#">
      <i class="chi-icon icon-atom" aria-hidden="true"></i>
      <span>Active Tab</span>
    </a>
  </li>
  <li>
    <a href="#">
      <i class="chi-icon icon-atom" aria-hidden="true"></i>
      <span>Tab link</span>
    </a>
  </li>
  <li>
    <a href="#">
      <i class="chi-icon icon-atom" aria-hidden="true"></i>
      <span>Tab link</span>
    </a>
  </li>
</ul>`
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
         code: `<ul class="chi-tabs -inverse -vertical -icons">
  <li class="-active">
    <a href="#">
      <i class="chi-icon icon-atom" aria-hidden="true"></i>
      <span>Active Tab</span>
    </a>
  </li>
  <li>
    <a href="#">
      <i class="chi-icon icon-atom" aria-hidden="true"></i>
      <span>Tab link</span>
    </a>
  </li>
  <li>
    <a href="#">
      <i class="chi-icon icon-atom" aria-hidden="true"></i>
      <span>Tab link</span>
    </a>
  </li>
</ul>`,
        }
           }
        },
      ],
    };
  },
})
export default class IconsVerticalLumenCenturyLink extends Vue {
  menuId = 'base';

  changeClosable(e: HeadTabsInterface) {
    this.menuId = e.id;
  }
}
</script>
