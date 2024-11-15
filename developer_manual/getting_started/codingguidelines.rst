=================================
Coding style & general guidelines
=================================

.. sectionauthor:: Bernhard Posselt <dev@bernhard-posselt.com>

General
-------

* Ideally, discuss your plans on the `forums <https://help.nextcloud.com>`_ to see if others want to work with you on it
* We use `GitHub <https://github.com/nextcloud>`_, please get an account there and clone the repositories you want to work on
* Fixes go directly to the main branch, nevertheless they need to be tested thoroughly.
* New features are always developed in a branch and only merged to the main branch once they are fully done.
* Software should work. We only put features into the main branch when they are complete.
  It's better to not have a feature instead of having one that works poorly.
* It is best to start working based on an issue - create one if there is none.
  You describe what you want to do, ask feedback on the direction you take it and take it from there.
* When you are finished, use the merge request function on GitHub to create a pull request.
  The other developers will look at it and give you feedback. You can signify that your PR is ready for review by adding the label "3. to review" to it.
  See `the code review page for more information <../prologue/bugtracker/codereviews.html>`_
* It is key to keep changes separate and small. The bigger and more hairy a PR grows, the harder it is to get it in.
  So split things up where you can in smaller changes - if you need a small improvement like a API addition for a big feature addition, get it in first rather than adding it to the big piece of work!
* Decisions are made by consensus. We strive for making the best technical decisions and as nobody can know everything, we collaborate.
  That means a first negative comment might not be the final word, neither is positive feedback an immediate GO. Nextcloud is built out of modular pieces (apps) and maintainers have a strong influence.
  In case of disagreement we consult other seasoned contributors.

Labels
------

We assign labels to issues and pull requests to make it easy to find them and to signal what needs to be done.
Some of these are assigned by the developers, others by QA, bug triagers, project lead or maintainers and so on.
It is not desired that users/reporters of bugs assign labels themselves, unless they are developers/contributors to Nextcloud.

The most important labels and their meaning:

* Tags showing the state of the issue or PR, numbered 0-4:

  * ``0. to triage`` - issue or feature request needs to get triaged and approved for development
  * ``1. to develop`` - ready to start development on this
  * ``2. developing`` - development in progress
  * ``3. to review`` - ready for review
  * ``4. to release`` - reviewed PR that awaits unfreeze of a branch to get merged or has pending CI jobs
  * ``needs info`` - this issue needs further information from the reporter, see :doc:`../../prologue/bugtracker/triaging`.
    This tag is typically combined with ``0. to triage`` to signal a bug report is not confirmed yet or a feature request has not been approved.

* Tags showing the type of issue or PR

  * ``bug`` - this issue is a bug
  * ``enhancement`` - this issue is a feature request/idea for improvement of Nextcloud
  * ``technical debt`` - this issue or PR is about `technical debt <https://en.wikipedia.org/wiki/Technical_debt>`_

* Tags that classify an issue or PR

  * ``high``, ``medium`` and ``low`` – signify how important the bug is.
  * ``regression`` - something that worked in a previous release but is now not working as expected or missing.
  * ``feature: *``, e.g. ``feature: dav`` – these tags group tickets of specific feature or subsystems.
  * ``design`` - this needs help from the design team or is a design-related issue/pull request
  * ``good first issue`` - these are issues which are relatively easy to solve and ideal for people who want to learn how to code in Nextcloud

* ``backport-request`` - the pull requests also needs to be applied to older Nextcloud versions. This tag is typically assigned by automation.

Coding
------

* Maximum line-length of 80 characters
* Use tabs to indent
* A tab is 4 spaces wide
* Opening braces of blocks are on the same line as the definition
* Quotes: ' for everything, " for HTML attributes (<p class="my_class">)
* End of Lines : Unix style (LF / '\n') only
* No global variables or functions
* Unit tests
* HTML should be HTML5 compliant
* When you ``git pull``, always ``git pull --rebase`` to avoid generating extra commits like: *merged main into main*

License headers
---------------

Nextcloud is licensed under the `GNU AGPLv3 <https://www.gnu.org/licenses/agpl>`_.
From June, 16 2016 on we switched to "GNU AGPLv3 or any later version" for better long-term maintainability.

If you create a new file please use this header:

.. code-block:: php

  /**
   * SPDX-FileCopyrightText: [year] [your name] [<your email address>]
   * SPDX-License-Identifier: AGPL-3.0-or-later
   */
   
The year should then be the creation time and the email address is optional.

If you edit an existing file please, please keep the existing license header as it is and just add your copyright notice, if you consider your changes substantial enough to claim copyright.

In order to do so there are two options:

* If a generic header is already present, please just add yourself to the AUTHORS.md file
* If no generic header is present, you can add yourself with a copyright line as described above. As a rule of thumb, this is the case if you contributed more than seven lines of code.

An example of a generic license header where adding yourself to the AUTHORS.md
file is preferred please see the example below

.. code-block:: php

  /**
   * SPDX-FileCopyrightText: 2024 Nextcloud GmbH and Nextcloud contributors
   * SPDX-License-Identifier: AGPL-3.0-or-later
   */

The Nextcloud GmbH part only applies to employees of the company not to contributors.

For more, general information on SPDX headers and their usage for reuse-compliance, please see 

* `REUSE <https://reuse.software/>`_
* `SPDX <https://spdx.dev/>`_

User interface
--------------

* Software should get out of the way. Do things automatically instead of offering configuration options.
* Software should be easy to use. Show only the most important elements. Secondary elements only on hover or via Advanced function.
* User data is sacred. Provide undo instead of asking for confirmation - `which might be dismissed <http://www.alistapart.com/articles/neveruseawarning/>`_
* The state of the application should be clear. If something loads, provide feedback.
* Do not adapt broken concepts (for example design of desktop apps) just for the sake of consistency. We aim to provide a better interface, so let's find out how to do that!
* Regularly reset your installation to see how the first-run experience is like. And improve it.
* Ideally do `usability testing <http://jancborchardt.net/usability-in-free-software>`_ to know how people use the software.
* For further UX principles, read `Alex Faaborg from Mozilla <http://uxmag.com/articles/quantifying-usability>`_.

PHP
---

Starting with Nextcloud 19 there is a shared `PHP Coding Standards Fixer <https://github.com/FriendsOfPhp/PHP-CS-Fixer>`_ configuration you can use to automatically format your app's source code. For full details see the `repository on GitHub <https://github.com/nextcloud/coding-standard/>`_.

Always use::

  <?php

at the start of your php code. The final closing::

  ?>

should not be used at the end of the file due to the `possible issue of sending white spaces <https://stackoverflow.com/questions/4410704/php-closing-tag>`_.

Comments
^^^^^^^^
All API methods need to be marked with `PHPDoc <https://en.wikipedia.org/wiki/PHPDoc>`_ markup. An example would be:

.. code-block:: php

  <?php

  /**
   * Description what method does
   * @param Controller $controller the controller that will be transformed
   * @param API $api an instance of the API class
   * @throws APIException if the api is broken
   * @since 4.5
   * @return string a name of a user
   */
  public function myMethod(Controller $controller, API $api) {
    // ...
  }

Objects, functions, arrays & variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use *UpperCamelCase* for Objects, *lowerCamelCase* for functions and variables. If you set
a default function/method parameter, do not use spaces. Do not prepend private
class members with underscores.

.. code-block:: javascript

  class MyClass {

  }

  function myFunction($default=null) {

  }

  $myVariable = 'blue';

  $someArray = array(
      'foo'  => 'bar',
      'spam' => 'ham',
  );

  ?>


Operators
^^^^^^^^^

Use **===** and **!==** instead of **==** and **!=**.

Here's why:

.. code-block:: php

  <?php

  var_dump(0 == "a"); // 0 == 0 -> true
  var_dump("1" == "01"); // 1 == 1 -> true
  var_dump("10" == "1e1"); // 10 == 10 -> true
  var_dump(100 == "1e2"); // 100 == 100 -> true

  ?>

Control structures
^^^^^^^^^^^^^^^^^^

* Always use { } for one line ifs
* Split long ifs into multiple lines
* Always use break in switch statements and prevent a default block with warnings if it shouldn't be accessed

.. code-block:: php

  <?php

  // single line if
  if ($myVar === 'hi') {
      $myVar = 'ho';
  } else {
      $myVar = 'bye';
  }

  // long ifs
  if (   $something === 'something'
      || $condition2
      && $condition3
  ) {
    // your code
  }

  // for loop
  for ($i = 0; $i < 4; $i++) {
      // your code
  }

  switch ($condition) {
      case 1:
          // action1
          break;

      case 2:
          // action2;
          break;

      default:
          // defaultaction;
          break;
  }

  ?>

Unit tests
^^^^^^^^^^

Unit tests must always extend the ``\Test\TestCase`` class, which takes care
of cleaning up the installation after the test.

If a test is run with multiple different values, a data provider must be used.
The name of the data provider method must not start with ``test`` and must end
with ``Data``.

.. code-block:: php

    <?php
    namespace Test;
    class Dummy extends \Test\TestCase {
        public function dummyData() {
            return array(
                array(1, true),
                array(2, false),
            );
        }

        /**
         * @dataProvider dummyData
         */
        public function testDummy($input, $expected) {
            $this->assertEquals($expected, \Dummy::method($input));
        }
    }


JavaScript and Typescript
-------------------------

There is a shared configuration for `eslint <https://eslint.org/>`_ that you can use to automatically format your Nextcloud apps's JavaScript code.
It consists of two parts: a `config package <https://github.com/nextcloud-libraries/eslint-config>`_ that contains the formatting preferences and a `plugin <https://github.com/nextcloud-libraries/eslint-plugin>`_ to detect deprecated and removed APIs in your code. See their readmes for instructions.

* Use a :file:`js/main.js` or :file:`js/app.ts` where your program is started
* Use **const** or **let** to limit variable to local scope
* Use JavaScript strict mode (automatically the case when using JavaScript modules)
* Use a global namespace object where you bind publicly used functions and objects to instead of plain global variables.

**DO**:

.. code-block:: javascript

  // set up namespace for sharing across multiple files
  var MyApp = MyApp || {};

  (function(window, $, exports, undefined) {
      'use strict';

      // if this function or object should be global, attach it to the namespace
      exports.myGlobalFunction = function(params) {
          return params;
      };

  })(window, jQuery, MyApp);


**DONT** (Seriously):

.. code-block:: javascript

  // This does not only make everything global but you're programming
  // JavaScript like C functions with namespaces
  MyApp = {
      myFunction:function(params) {
          return params;
      },
      ...
  };

Objects & inheritance
^^^^^^^^^^^^^^^^^^^^^

Try to use OOP in your JavaScript to make your code reusable and flexible.

This is how you'd do inheritance in JavaScript:

.. code-block:: javascript

  class ParentClass {
      // a public property
      name;
      // names prefixed with # are private in JavaScript and can not be accessed from outside
      // #privateProperty;

      constructor(name) {
          this.name = name;
      }

      sayHello() {
          console.log(this.name);
      }
  }

  class ChildClass extends ParentClass {
      age;

      constructor(name, age) {
          super(name);
          this.age = age;
      }

      // overwrite parent method
      sayHello() {
          console.log('child class: ', this.name, this.age);
      }
  }

  const child = new ChildClass('toni', 23)
  // Prints: child class: toni 23
  child.sayHello();

Objects, functions & variables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use *UpperCamelCase* for Objects, *lowerCamelCase* for functions and variables.

.. code-block:: javascript

  const MyObject = function() {
      this.attr = "hi";
  };

  const myFunction = function() {
      return true;
  };

  const myVariable = 'blue';

  const objectLiteral = {
      value1: 'somevalue',
  };


Operators
^^^^^^^^^

Use **===** and **!==** instead of **==** and **!=**.

Here's why:

.. code-block:: javascript

  '' == '0'           // false
  0 == ''             // true
  0 == '0'            // true

  false == 'false'    // false
  false == '0'        // true

  false == undefined  // false
  false == null       // false
  null == undefined   // true

  ' \t\r\n ' == 0     // true

Control structures
^^^^^^^^^^^^^^^^^^

* Always use { } for one line ifs
* Split long ifs into multiple lines
* Always use break in switch statements and prevent a default block with warnings if it shouldn't be accessed

**DO**:

.. code-block:: javascript

  // single line if
  if (myVar === 'hi') {
      myVar = 'ho';
  } else {
      myVar = 'bye';
  }

  // long ifs
  if (   something === 'something'
      || condition2
      && condition3
  ) {
    // your code
  }

  // for loop
  for (let i = 0; i < 4; i++) {
      // your code
  }

  // switch
  switch (value) {

      case 'hi':
          // your code
          break;

      default:
          console.warn('Entered undefined default block in switch');
          break;
  }


CSS
---

- Do not bind your CSS to much to your HTML structure.
- Try to avoid IDs.
- Try to make your CSS reusable by grouping common attributes into classes.
- Take a look at the `Writing Tactical CSS & HTML <https://www.youtube.com/watch?v=hou2wJCh3XE&feature=plcp>`_ video on YouTube.

**DO**:

.. code-block:: css

  .list {
      list-style-type: none;
  }

  .list > .list__item {
      display: inline-block;
  }

  .important_list_item {
      color: red;
  }

**DON'T**:

.. code-block:: css

  #content .myHeader ul {
      list-style-type: none;
  }

  #content .myHeader ul li.list_item {
      color: red;
      display: inline-block;
  }

Naming convention
^^^^^^^^^^^^^^^^^

We recommend to use the BEM (Block-Element-Modifier) naming convention for CSS classes.
BEM helps with making CSS reusable and better maintainable, especially when using pre-processors like SASS.

**DO**:

.. code-block:: css

  .button {
      background-color: var(--color-main-background);
  }

  .button--primary {
      background-color: var(--color-primary);
  }

  .button__icon {
      width: 20px;
  }

**DON'T**:

.. code-block:: css

  button.btn {
      background-color: var(--color-main-background);
  }

  button.btn.primary {
      background-color: var(--color-primary);
  }
  button.btn span.myIcon {
      width: 20px;
  }
