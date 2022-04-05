<template lang="pug">
  <ComponentExample title="Wait for animations" :id="exampleId" :tabs="exampleTabs" :headTabs="headTabs" @chiHeadTabsChange="e => changeClosable(e)">
    p.-text(slot="example-description")
      | Browsers stop any execution of JavaScript as soon as a link is clicked and it starts to fetch the destination URL.
      | For this reason, the sliding border animation will not be perceived by the user when an external link is clicked, as
      | the animation will not be done, an this can be confusing for the user. To prevent this possible confusion, this
      | component has the option to wait for the animation to finish and, then, it will redirect the user to the destination
      | URL. You can enable this behavior by setting the <code>waitForAnimations</code> option to <code>true</code>.

    .div(slot="example")
      ul.chi-tabs.chi-navigationExample.chi-customExample
        li(:class="index === 0 ? '-active' : ''" v-for="(link, index) in tabLinks")
          a(:href="`?tab=${index + 1}`") {{ link }}      
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

@Component({
  data: () => {
    return {
      exampleId: 'wait-animations-lumen-centurylink',
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
      tabLinks: Array(6).fill('Tab Link'),
      headTabs: [
        {
          active: true,
          id: 'enable',
          label: 'Enabled',
            codeSnippets: {
        webComponent: {
          code: ''
        },
        htmlBlueprint: {
          code: `<ul id="navigationexample-4-enabled" class="chi-tabs">
  <li class="-active">
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
</ul>
<script>
const navigationElem = document.getElementById('#navigationexample-4-enabled');
chi.navigation(
  navigationElem,
  {waitForAnimations: true}
);
<\/script>`,
        }
            }
        },
        {
          id: 'disable',
          label: 'Disabled',
          codeSnippets: {
        webComponent: {
          code: ''
        },
        htmlBlueprint: {
         code: `<ul id="navigationexample-4-disabled" class="chi-tabs">
  <li class="-active">
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
  <li>
    <a href="/">Tab Link</a>
  </li>
</ul>
<script>
  const navigationElem = document.getElementById('#navigationexample-4-disabled');
  chi.navigation(
    navigationElem,
    {waitForAnimations: false}
  );
<\/script>`
        },
      },
        },
      ],
      
    };
  },
})
export default class WaitAnimationsLumenCenturyLink extends Vue {
  menuId = 'enable';

  changeClosable(e: HeadTabsInterface) {
    this.menuId = e.id;
  }
}
</script>
