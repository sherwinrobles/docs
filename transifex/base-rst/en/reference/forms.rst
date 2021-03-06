%{forms_268d46b16a1976672dfca0eb3004a1c6}%
=====
%{forms_c8d311b9dc231bba212a1daa1a334929}%

%{forms_09046bd05925c7ff83bddee4094d745a}%

.. code-block:: php

    <?php

    use Phalcon\Forms\Form,
        Phalcon\Forms\Element\Text,
        Phalcon\Forms\Element\Select;

    $form = new Form();

    $form->add(new Text("name"));

    $form->add(new Text("telephone"));

    $form->add(new Select("telephoneType", array(
        'H' => 'Home',
        'C' => 'Cell'
    )));

%{forms_893e7de61da03f27bf81496bea047a78}%

.. code-block:: html+php

    <h1>Contacts</h1>

    <form method="post">

        <p>
            <label>Name</label>
            <?php echo $form->render("name") ?>
        </p>

        <p>
            <label>Telephone</label>
            <?php echo $form->render("telephone") ?>
        </p>

        <p>
            <label>Type</label>
            <?php echo $form->render("telephoneType") ?>
        </p>

        <p>
            <input type="submit" value="Save" />
        </p>

    </form>

%{forms_e2b94867ac1d9e19c574de4ca3f94731}%

.. code-block:: html+php

    <p>
        <label>Name</label>
        <?php echo $form->render("name", array('maxlength' => 30, 'placeholder' => 'Type your name')) ?>
    </p>

%{forms_ae156d94a8f7c96ac0e8477e37df4225}%

.. code-block:: php

    <?php

    $form->add(new Text("name", array(
        'maxlength' => 30,
        'placeholder' => 'Type your name'
    )));

%{forms_b6a77d0fb8bf4d24a2041c6dc533b9c9}%
------------------
%{forms_46118ce7551fd5b99ce1494d067d7e35}%

.. code-block:: php

    <?php

    use Phalcon\Forms\Form,
        Phalcon\Forms\Element\Text,
        Phalcon\Forms\Element\Select;

    class ContactForm extends Form
    {
        public function initialize()
        {
            $this->add(new Text("name"));

            $this->add(new Text("telephone"));

            $this->add(new Select("telephoneType", TelephoneTypes::find(), array(
                'using' => array('id', 'name')
            )));
        }
    }

:doc:`Phalcon\\Forms\\Form <../api/Phalcon_Forms_Form>` extends :doc:`Phalcon\\DI\\Injectable <../api/Phalcon_DI_Injectable>`
%{forms_b66e4848b3bda7c0e8df7255d7a1d005}%

.. code-block:: php

    <?php

    use Phalcon\Forms\Form,
        Phalcon\Forms\Element\Text,
        Phalcon\Forms\Element\Hidden;

    class ContactForm extends Form
    {

        /**
         * This method returns the default value for field 'csrf'
         */
        public function getCsrf()
        {
            return $this->security->getToken();
        }

        public function initialize()
        {

            //{%forms_3d8efd11b40598f9eda1d29b58b8dbc6%}
            $this->setEntity($this);

            //{%forms_4ee594653745ac582ff5c9a44298e2bc%}
            $this->add(new Text("email"));

            //{%forms_8349f54e05d647e20b8c77ee17f5cfd4%}
            $this->add(new Hidden("csrf"));
        }
    }

%{forms_69a37c891f1c62b554a342c50a6a3cf8}%

.. code-block:: php

    <?php

    use Phalcon\Forms\Form,
        Phalcon\Forms\Element\Text,
        Phalcon\Forms\Element\Hidden;

    class UsersForm extends Form
    {
        /**
         * Forms initializer
         *
         * @param Users $user
         * @param array $options
         */
        public function initialize($user, $options)
        {

            if ($options['edit']) {
                $this->add(new Hidden('id'));
            } else {
                $this->add(new Text('id'));
            }

            $this->add(new Text('name'));
        }
    }

%{forms_1829d8e5d10a665bd39d5dc5b4696b02}%

.. code-block:: php

    <?php

    $form = new UsersForm(new Users(), array('edit' => true));

%{forms_c81f893f5539efed7a6b2aae2d783e35}%
----------
%{forms_39b4103e3d92d2c731cbba3666242870}%

.. code-block:: php

    <?php

    use Phalcon\Forms\Element\Text,
        Phalcon\Validation\Validator\PresenceOf,
        Phalcon\Validation\Validator\StringLength;

    $name = new Text("name");

    $name->addValidator(new PresenceOf(array(
        'message' => 'The name is required'
    )));

    $name->addValidator(new StringLength(array(
        'min' => 10,
        'messageMinimum' => 'The name is too short'
    )));

    $form->add($name);

%{forms_a7fe5ae6c44cbf9fe34b36a02be1be0e}%

.. code-block:: php

    <?php

    if (!$form->isValid($_POST)) {
        foreach ($form->getMessages() as $message) {
            echo $message, '<br>';
        }
    }

%{forms_8cfec398b55e710d9604a7c436050be6}%

%{forms_587c4ff197b622b3c1ed93b253343404}%

.. code-block:: php

    <?php

    foreach ($form->getMessages(false) as $attribute => $messages) {
        echo 'Messages generated by ', $attribute, ':', "\n";
        foreach ($messages as $message) {
            echo $message, '<br>';
        }
    }

%{forms_3fb3ea3db05b9e1080de859d46f0b814}%

.. code-block:: php

    <?php

    foreach ($form->getMessagesFor('name') as $message) {
        echo $message, '<br>';
    }

%{forms_6cfe651493a752780c8fa48b71bdc818}%
---------
%{forms_d52da57fff163b8d574cc0bb032dfd7d}%

%{forms_b2030575ebc9fde0b4c6ea3a4625fbd6}%
--------------------
%{forms_b91be4cb2b5626cabb9965b2a0858548}%

.. code-block:: php

    <?php

    $robot = Robots::findFirst();

    $form = new Form($robot);

    $form->add(new Text("name"));

    $form->add(new Text("year"));

%{forms_b28bcc0439b5154f7ed057f8489f90e5}%

.. code-block:: html+php

    <?php echo $form->render('name') ?>

%{forms_6da412a2f660aebd78578e72791688d0}%

.. code-block:: php

    <?php

    $form->bind($_POST, $robot);

    //{%forms_1af24ac4da1919c6fede2e6146c56fdc%}
    if ($form->isValid()) {

        //{%forms_0e4c7d0119ba09c444ac1079f86cc679%}
        $robot->save();
    }

%{forms_d30a6b17040285931e0f8c947d33cfa3}%

.. code-block:: php

    <?php

    class Preferences
    {

        public $timezone = 'Europe/Amsterdam';

        public $receiveEmails = 'No';

    }

%{forms_97eb3ee480823a9a95735e9608c7a797}%

.. code-block:: php

    <?php

    $form = new Form(new Preferences());

    $form->add(new Select("timezone", array(
        'America/New_York' => 'New York',
        'Europe/Amsterdam' => 'Amsterdam',
        'America/Sao_Paulo' => 'Sao Paulo',
        'Asia/Tokyo' => 'Tokyo',
    )));

    $form->add(new Select("receiveEmails", array(
        'Yes' => 'Yes, please!',
        'No' => 'No, thanks'
    )));

%{forms_baf2a1f8830086140eebac87fdb93e9c}%

.. code-block:: php

    <?php

    class Preferences
    {

        public $timezone;

        public $receiveEmails;

        public function getTimezone()
        {
            return 'Europe/Amsterdam';
        }

        public function getTimezone()
        {
            return 'No';
        }

    }

%{forms_267733a64ba9eb261ead15feedb03145}%
-------------
%{forms_955db7b1fad92c1ef8cecdf5046a7e4b}%

+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Name         | Description                                                                                                                                                      | Example                                                           |
+==============+==================================================================================================================================================================+===================================================================+
| Text         | Generate INPUT[type=text] elements                                                                                                                               | :doc:`Example <../api/Phalcon_Forms_Element_Text>`                |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Password     | Generate INPUT[type=password] elements                                                                                                                           | :doc:`Example <../api/Phalcon_Forms_Element_Password>`            |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Select       | Generate SELECT tag (combo lists) elements based on choices                                                                                                      | :doc:`Example <../api/Phalcon_Forms_Element_Select>`              |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Check        | Generate INPUT[type=check] elements                                                                                                                              | :doc:`Example <../api/Phalcon_Forms_Element_Check>`               |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Textarea     | Generate TEXTAREA elements                                                                                                                                       | :doc:`Example <../api/Phalcon_Forms_Element_TextArea>`            |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Hidden       | Generate INPUT[type=hidden] elements                                                                                                                             | :doc:`Example <../api/Phalcon_Forms_Element_Hidden>`              |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| File         | Generate INPUT[type=file] elements                                                                                                                               | :doc:`Example <../api/Phalcon_Forms_Element_File>`                |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Date         | Generate INPUT[type=date] elements                                                                                                                               | :doc:`Example <../api/Phalcon_Forms_Element_Date>`                |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Numeric      | Generate INPUT[type=number] elements                                                                                                                             | :doc:`Example <../api/Phalcon_Forms_Element_Numeric>`             |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+
| Submit       | Generate INPUT[type=submit] elements                                                                                                                             | :doc:`Example <../api/Phalcon_Forms_Element_Submit>`              |
+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------+

%{forms_e645d2a669a3a9bcdd068f9166964e8c}%
---------------
%{forms_19c30705d1c08473182f5ca8868cb348}%

.. code-block:: html+php

    <?php

    class ContactForm extends Phalcon\Mvc\Form
    {
        public function beforeValidation()
        {

        }
    }

%{forms_eb42718fc9fd2cd9c708358693722c8f}%
---------------
%{forms_4604a283537fa2bcbe51f858027d2fc8}%

.. code-block:: html+php

    <?php

    <form method="post">
        <?php
            //{%forms_d2e174e2f09ade4279de5d7701ed3131%}
            foreach ($form as $element) {

                //{%forms_ab27bfb50aa900c676b49acb9ed5bfe7%}
                $messages = $form->getMessagesFor($element->getName());

                if (count($messages)) {
                    //{%forms_945d58b527860c5a740921dd3d689c0e%}
                    echo '<div class="messages">';
                    foreach ($messages as $message) {
                        echo $message;
                    }
                    echo '</div>';
                }

                echo '<p>';
                echo '<label for="', $element->getName(), '">', $element->getLabel(), '</label>';
                echo $element;
                echo '</p>';

            }
        ?>
        <input type="submit" value="Send"/>
    </form>

%{forms_e996858ec164c2b15da16cb43a8ad731}%

.. code-block:: php

    <?php

    class ContactForm extends Phalcon\Forms\Form
    {
        public function initialize()
        {
            //...
        }

        public function renderDecorated($name)
        {
            $element = $this->get($name);

            //{%forms_ab27bfb50aa900c676b49acb9ed5bfe7%}
            $messages = $this->getMessagesFor($element->getName());

            if (count($messages)) {
                //{%forms_945d58b527860c5a740921dd3d689c0e%}
                echo '<div class="messages">';
                foreach ($messages as $message) {
                    echo $this->flash->error($message);
                }
                echo '</div>';
            }

            echo '<p>';
            echo '<label for="', $element->getName(), '">', $element->getLabel(), '</label>';
            echo $element;
            echo '</p>';
        }

    }

%{forms_65089c75f285a799c01cf5255970f306}%

.. code-block:: php

    <?php

    echo $element->renderDecorated('name');

    echo $element->renderDecorated('telephone');

%{forms_99367eefd1b35e19421d526542d01dc9}%
----------------------
%{forms_e75214c5550dd80b0ed2d3cb0d17fad5}%

.. code-block:: php

    <?php

    use Phalcon\Forms\Element;

    class MyElement extends Element
    {
        public function render($attributes=null)
        {
            $html = //{%forms_49e9eeca1ccfd6d04a641dce3a4b8956%}
            return $html;
        }
    }

%{forms_f44949bed8f1275638b7022df8e51ed7}%
-------------
%{forms_f0111160333068fb652bd469bd43a195}%

.. code-block:: php

    <?php

    $di['forms'] = function() {
        return new Phalcon\Forms\Manager();
    };

%{forms_3ad2f73417ccd3fdc7714a4f13f3f4c5}%

.. code-block:: php

    <?php

    $this->forms->set('login', new LoginForm());

%{forms_04054dc72bd09b7854bfcdbf3be94cd4}%

.. code-block:: php

    <?php

    echo $this->forms->get('login')->render();

