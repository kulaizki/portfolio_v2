<script lang="ts">
  import SkillItem from "$lib/components/SkillItem.svelte";
  export let className: string = '';
  import { cubicOut } from "svelte/easing";
  import { inview } from 'svelte-inview';
	let isInView = false;
  let hasAnimated = false;

  function blurFly(node: HTMLElement, params: { 
    delay?: number, 
    duration?: number, 
    easing?: (t: number) => number 
  } = {}): { 
    delay: number, 
    duration: number, 
    easing: (t: number) => number, 
    css: (t: number) => string 
  } {
    const existingTransform = getComputedStyle(node).transform.replace('none', '');
    return {
      delay: params.delay || 0,
      duration: params.duration || 1000,
      easing: params.easing || cubicOut,
      css: (t: number) => `
        transform: ${existingTransform} translateY(${(1 - t) * 100}px);
        opacity: ${t};
        filter: blur(${(1 - t) * 10}px);
      `
    };
  }
</script>

<section 
  id="skills" 
  class="py-20 text-white {className}"
	use:inview={{ threshold: 0.3 }}
	on:inview_change={(event) => {
    if (!hasAnimated) {
      isInView = event.detail.inView;
      if (isInView) hasAnimated = true;
    }
  }}
>
  {#if isInView}
    <div 
      class="mx-auto max-w-6xl px-6" 
      transition:blurFly
    >
      <h2 class="text-3xl md:text-4xl font-bold text-center mb-16">Skills</h2>
      <div class="flex flex-wrap justify-center gap-6">
        <SkillItem skillName="Svelte" skillUrl="https://svelte.dev/" skillIcon="https://skillicons.dev/icons?i=svelte" />
        <SkillItem skillName="Next.js" skillUrl="https://nextjs.org/" skillIcon="https://skillicons.dev/icons?i=nextjs" />
        <SkillItem skillName="React" skillUrl="https://reactjs.org/" skillIcon="https://skillicons.dev/icons?i=react" />
        <SkillItem skillName="Tailwind" skillUrl="https://tailwindcss.com/" skillIcon="https://skillicons.dev/icons?i=tailwind" />
        <SkillItem skillName="Typescript" skillUrl="https://www.typescriptlang.org/" skillIcon="https://skillicons.dev/icons?i=javascript" />
        <SkillItem skillName="Javascript" skillUrl="https://www.javascript.com/" skillIcon="https://skillicons.dev/icons?i=typescript" />
        <SkillItem skillName="Supabase" skillUrl="https://supabase.io/" skillIcon="https://skillicons.dev/icons?i=supabase" />
        <SkillItem skillName="Firebase" skillUrl="https://firebase.google.com/" skillIcon="https://skillicons.dev/icons?i=firebase" />
        <SkillItem skillName="Git" skillUrl="https://git-scm.com/" skillIcon="https://skillicons.dev/icons?i=git" />
        <SkillItem skillName="Vercel" skillUrl="https://vercel.com/" skillIcon="https://skillicons.dev/icons?i=vercel" />
        <SkillItem skillName="Linux" skillUrl="https://www.linux.org/" skillIcon="https://skillicons.dev/icons?i=linux" />
        <SkillItem skillName="AWS" skillUrl="https://aws.amazon.com/" skillIcon="https://skillicons.dev/icons?i=aws" />
        <SkillItem skillName="Python" skillUrl="https://www.python.org/" skillIcon="https://skillicons.dev/icons?i=python" />
        <SkillItem skillName="SQL" skillUrl="https://www.mysql.com/" skillIcon="https://skillicons.dev/icons?i=mysql" />
        <SkillItem skillName="TensorFlow" skillUrl="https://www.tensorflow.org/" skillIcon="https://skillicons.dev/icons?i=tensorflow" />
        <SkillItem skillName="Figma" skillUrl="https://www.figma.com/" skillIcon="https://skillicons.dev/icons?i=figma" />
      </div>
    </div>
  {/if}
</section>
