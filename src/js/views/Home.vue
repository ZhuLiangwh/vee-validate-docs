<template>
    <div>
        <h2 id="about" class="title is-4"><a href="#about">What is vee-validate?</a></h2>
        <p>
            This is a lightweight plugin for <a href="https://vuejs.org/" class="link">Vue.js</a> that allows you to validate input fields, and display errors.
            <br><br>
            You don't have to do anything fancy in your app, most of the work goes into the html.
            You only need to specify for each input what kind of validators should be used when the value changes. You will then get informed of the errors for each field.
            <br><br>
            Although most of the validations occur automatically, you can use the validator however you see fit. The validator object has no dependencies and is a standalone object.
            <br><br>
            Currently there are over 20 validation rules available in the plugin.
            This plugin is inspired by <a href="https://laravel.com/" class="link">PHP Framework Laravel's validation syntax</a>.
            <br><br>It also supports Vue 2.0. All examples here are built using Vue 2.0 with the plugin.
        </p>
        <h2 id="installation" class="title is-4"><a href="#installation">Installation</a></h2>
        <p>
            You can install this plugin via <a class="link" href="#npm">npm</a> or <a class="link" href="#bower">bower</a> or via a <a class="link" href="#cdn">CDN</a>.
            <h2 id="npm" class="title is-4"><a href="#npm">npm</a></h2>
            <b>Vue 1.x</b>
            <code-block class="language-bash">npm install vee-validate --save</code-block>
            <b>Vue 2.x</b>
            <code-block class="language-bash">npm install vee-validate@next --save</code-block>

            <h2 id="bower" class="title is-4"><a href="#bower">bower</a></h2>
            <b>Vue 1.x</b>
            <code-block class="language-bash">bower install vee-validate#1.0.0-beta.10 --save</code-block>
            <b>Vue 2.x</b>
            <code-block class="language-bash">bower install vee-validate#2.0.0-beta.15 --save</code-block>

            <h2 id="cdn" class="title is-4"><a href="#cdn">CDN</a></h2>
            Head over to <a href="https://www.jsdelivr.com/projects/vee-validate" target="jsdelivr">jsdelivr</a> and grab the latest version.

            Then you may use it like this:
            <code-block class="language-html">
                &lt;script src=&quot;path/to/vue.js&quot;&gt;&lt;/script&gt;
                &lt;script src=&quot;path/to/vee-validate.js&quot;&gt;&lt;/script&gt;
                &lt;script&gt;
                    Vue.use(VeeValidate); // good to go.
                &lt;/script&gt;
            </code-block>

            or you may import it using ES6:
            <code-block class="language-javascript">
                import Vue from 'vue';
                import VeeValidate from 'vee-validate';

                Vue.use(VeeValidate);
            </code-block>
        </p>
        <h2 id="basic-example" class="title is-4"><a href="#basic-example">Basic Example</a></h2>
        <p>
            All you need is to add the <code class="inline">v-validate</code> directive to the input you wish to validate.
            <br><br>
            Then add a <code class="inline">data-vv-rules</code> attribute which contains a list of validation rules separated by a pipe '<code class="inline">|</code>'.
            For the following example the validation rules are straight forward, use <code class="inline">required</code> to indicate that the field is required.
            And <code class="inline">email</code> to indicate that the field must be an email.
            To combine both rules we assign the value <code class="inline">required|email</code> to the <code class="inline">data-vv-rules</code> data-vv-set attribute.
        </p>
        <basic-example></basic-example>
        <div class="flex-center"><router-link class="link" :to="{ name: 'examples' }">More Examples</router-link></div>
        <br>
        <note title="Note">
            The field name that appears in the error messages is usually the input's <code>name</code> attribute, unless you passed a value from the vue instance <code>$data</code> object,
            The name will be then the expression name, check the <router-link :to="{ name: 'examples', hash: '#validate-data-vv-example' }">data validation example</router-link>.
        </note>
        <note>
            Its always a good idea to have a <code>name</code> attribute on your fields. If you are not binding the field and do not have a name attribute the validator won't properly register the field.
        </note>
        <h2 id="render-errors" class="title is-4"><a href="#render-errors">Rendering Errors</a></h2>
        <p>
            Naturally, you would want to display the errors to your users. The plugin augments your Vue instance with a private validator object and a public errors data object.
            You are responsible for how the errors should be rendered.
            <br><br>The errors object exposes a simple methods to help you render errors:
            <ul class="list-circle">
                <li><code class="inline">first('field')</code> Fetches the first error message associated with that field.</li>
                <li><code class="inline">collect('field')</code> Fetches all error messages associated with that field. alternativly you can pass nothing and it will return errors grouped by fields</li>
                <li><code class="inline">has('field')</code> Checks if there are any errors associated with that field.</li>
                <li><code class="inline">all()</code> Gets all error messages.</li>
                <li><code class="inline">any()</code> Checks if there are any errors.</li>
            </ul>
            There are a few more <router-link class="link" :to="{ name: 'api', hash: '#error-bag'}">methods</router-link> that you can use to manipulate the errors object.
        </p>
        <h2 id="available-rules" class="title is-4"><a href="#available-rules">Available Rules</a></h2>
        <p>There are more than 20 rules available to validate your inputs:</p>
        <div class="columns is-multiline">
            <div v-for="group in rules" :class="'column is-' + 12 / rules.length">
                <ul class="list-circle">
                    <li v-for="rule in group"><router-link class="link" :to="{ name: 'rules', hash: '#rule-' + rule }">{{ rule }}</router-link></li>
                </ul>
            </div>
        </div>
        <p>Visit the <router-link class="link" :to="{ name: 'rules', hash: '#available-rules' }">rules documentation</router-link> to learn more about how to use each rule, and how to <router-link :to="{ name: 'rules', hash: '#custom-rules' }" class="link">create your own</router-link>.</p>
        <h2 id="configuration" class="title is-4"><a href="#configuration">Configuration</a></h2>
        <p>
            You may need to configure some options to tweak some of the plugin internals, this is not required, but could cause conflicts. For example: if you are using a property called <code class="inline">errors</code> on your vue instance this may cause conflicts.
             Here is how you would set up the options along with the default values:
        </p>
        <code-block class="language-javascript">
            import Vue from 'vue';
            import VeeValidate from 'vee-validate';

            const config = {
                errorBagName: 'errors', // change if property conflicts.
                delay: 0,
                locale: 'en',
                messages: null,
                strict: true
            };

            Vue.use(VeeValidate, config);
        </code-block>
        <ul class="list-circle">
            <li><code class="inline">errorBagName:</code> The name of the ErrorBag object that will be injected in each of Vue's instances' data.</li>
            <li><code class="inline">delay:</code> The default debounce time for all inputs (only affects validations).</li>
            <li><code class="inline">locale:</code> The default language for the validation messages.</li>
            <li><code class="inline">messages:</code> The messages to be generated for the validation errors, check <router-link class="link" :to="{ name: 'rules', hash: '#custom-messages' }">custom messages</router-link> section.</li>
            <li><code class="inline">strict:</code> Fields that have no rules will fail validation unless <code class="inline">strict</code> is set to false.</li>
        </ul>
    </div>
</template>

<script>
import Collection from 'collectionsjs';
import data from './../data.json';
import BasicExample from './../components/examples/Basic.vue';

export default {
    data: () => ({
        rules: new Collection(data.rules).chunk(10).all()
    }),
    components: {
        BasicExample
    }
};
</script>
