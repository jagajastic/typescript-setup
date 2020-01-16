# typescript-setup
Simple step by step way to setup typescript for nodejs and express

## Typescript - A superset of JS that lets you add types to your code and get autocompletion. Documentation is at https://www.typescriptlang.org/

<code>If you use NPM
npm install --save-dev typescript # To install the module</code>

or

<code>
If you use yarn
yarn add --dev typescript
</code>


<code>npx tsc --init # to create a typescript config
npx tsc # to build/compile/transpile your typescript project
npx tsc -w # to setup typescript compilation in watch mode
</code>


You then need to install typings. Most typings are in the `@types/` module scope and you DO NOT import them in your projects, its just for typescript to figure out declarations for modules.

To check the typings for any module, use the http://aka.ms/types website to search.
You can install typings in your project using npm

<code>
npm i --save-dev @types/node @types/express</code>


or 


<code>yarn
yarn add --dev @types/node @types/express
  </code>
  
  
  
To install the node and express typings for example.

Keep in mind that for modules that are already scoped, ie. modules that start with @something/module, the typings for those projects are usually replaced with __ (that's two underscore). For example, the typings for @hapi/joi would be @types/hapi__joi.

## ts-jest - A module that lets jest understand typescript.
Documentation is at https://kulshekhar.github.io/ts-jest/

Jest - our code runner of choice - by default runs code with node, which only understands typescript. ts-jest makes jest run your code through typescript first for transpilation before being run in node.

A best practice is to write tests for your projects and to run your tests against the code your wrote, not the transpiled one: although there might be cases where that is worthwhile.

To install ts-jest, you should already have jest and its typings installed.

To install the required modules for testing a typescript project, 

Run, if using npm

<code>
npm i --save-dev jest @types/jest ts-jest
  </code>
  
  
If you're using yarn, do

<code>
yarn add --dev jest @types/jest ts-jest
  </code>


Next, we need to configure jest to use ts-jest to run our projects. So, we need to create a jest config. We can have ts-jest do that automatically for us, by running


<code>
npx ts-jest config:init
</code>


This creates a jest.config.js file in your project. You can now write your tests using typescript. Note that, by default, ts-jest is only configured to run typescript files, so, make sure your tests have the .ts file extension.

## express-generator - A module to quickly bootstrap an express project.

Bootstrap a new express project, by running

<code>npx express-generator</code>


In the folder you want your project created in.

Note that by default, the project created is configured for isomorphic rendering or server side rendering, using jade. If you don't need that feature, you can remove it.

## supertest - A module for running express integration tests

Documentation is at https://github.com/visionmedia/supertest

Jest is our test runner of choice, but for testing our web server routes, we would like to mock out the http server. So, we can just test the routes like a user would without the overhead of creating an http server in node.

To install the module run, using npm

<code>
npm i --save-dev supertest @types/supertest</code>


Or, using yarn


<code>yarn add --dev supertest @types/supertest</code>



Keep in mind that its jest that still runs the test, supertest just mocks an http server and makes it easy to test.

In your test file, import your express app, if you're using express-generator, that's your app.js or app.ts file.

supertest exports a function that returns a promise and lets you do assertions. So, you'd use it as shown below in jest.


<code>import request from 'supertest'
import app from 'src/app'

test('it allows a get request', () => {
  return request(app)
    .get('/api/welcome')
    .expect(200);
});
</code>



Notice how the request function is returned, this important in jest. A different way of writing the same thing, without is


<code>
import request from 'supertest'
import app from 'src/app'

test('it allows a get request', () => {
  return request(app)
    .get('/api/welcome')
    .expect((res) => {
      expect(res.status).toBe(200);
    });
});
</code>



See the documentation for details.

## Others
We also, used 

joi - @hapi/joi - for validation, using schemas.
prettier, pretty-quick, husky - for beautifying code on commit.
