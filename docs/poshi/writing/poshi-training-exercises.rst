========================
Poshi Training Exercises
========================

.. note::
  Taken from Brazil Training 2021
  
1. Follow the tutorial in the `Learn Poshi section`_. Your portal is already located at ``/home/me/dev/projects/liferay-portal``.

2. Understand and explain what the following scripts do (level: 2.1 to 2.4 = easy, 2.5 to 2.8 = moderate). Go to the `Forms test directory`_. These tests are available in Forms.testcase.

  #. test AddFormWithDuplicateTextFields
  #. test CanBeUnpublished
  #. test ConfigureAutosave
  #. test PagesCanBeReordered
  #. test EditAllFormFieldsTypesUsedBySystemSettings
  #. test SelectAndRemoveMultipleOptionsInSelectFromListField
  #. test SubmitFormAndViewEmailNotification
  #. test SubmitFormWithAllFieldTypesAndThreePages
    
3. Run an existing test.
  
  #. Launch the portal;
  #. Go to the portal home;
  #. Run ``ant -f build-test.xml run-selenium-test -Dtest.class=FILE#TEST_METHOD`` where FILE is the name of the file where the TEST_METHOD is located.
  
    Example: ``ant -f build-test.xml run-selenium-test -Dtest.class=Forms#AddFormWithDuplicateTextFields``
  
  .. tip::
    **How to speed up your test execution**

    #. Go to the portal home;
    #. Create the following file: ``test.<your-user-name>.properties``
    #. Add the following code snippet::
    
        timeout.explicit.wait=10
        test.assert.console.errors=false
    
    Default timeout.explicit.wait is 120 seconds - this is the time poshi will wait for an element. Default assert console error is true - reading log makes poshi slower.
      
4. Download IDE according to your preference.
  
  * Sublime Text 3 or VS Code;
  * We recommend scoping your portalweb folder into a project;
  * Set the language association of ``*.testcases``, ``*.macros`` to Groovy and ``*.paths`` to XML for a better content visualization.

5. Steps to create a new test.
  
  1. Go to portal-web/test/functional/com/liferay/portalweb/tests/
  2. Create a folder sample
  3. Create a file MyTestFile.testcase
  4. Add the following code snippet::
      
        @component-name = "app-builder"
        definition {
            property testray.main.component.name = "App Builder";
        
            setUp {
                TestCase.setUpPortalInstance();
        
                User.firstLoginPG();
        
                Navigator.openURL();
            }
        
            tearDown {
                User.logoutAndLoginPG(
                    userLoginEmailAddress = "test@liferay.com",
                    userLoginFullName = "Test Test");
            }
        
            @description = "Access Portal Global Menu and validate CONFIGURATION string at Control Panel"
            @priority = "5"
            test ValidateConfigurationStringAtControlPanel {
        
        
            }
        
            @description = "Set Screen size to custom and validate values"
            @priority = "5"
            test SetScreenSizeAndValidateValues {
        
        
            }
        }
  5. Open the terminal and execute the following command: ``ant -f build-test.xml run-selenium-test -Dtest.class=MyTestFile#ValidateConfigurationStringAtControlPanel`` or ``ant -f build-test.xml run-selenium-test -Dtest.class=MyTestFile#SetScreenSizeAndValidateValues``.
  
  6. Implement the tests (next topic)
  
6. Creating sample tests (based on file created in the previous topic).
  
  **Validating a string**
  
    1. Open portal;  
    2. Open the Global Menu (top right corner - );
    3. Switch to Control Panel option;
    4. Assert "CONFIGURATION" section is shown.
  
  **Inputting values**
  
    1. Open the portal;
    2. Open the Simulation menu (top right corner - );
    3. Change the Screen Size to Custom;
    4. Set the Height (px) to 1920 px and Width (px) to 1080 px;
    5. Close the Simulation menu;
    6. Reopen the Simulation menu;
    7. Assert the values previously set are persisted.
  
  
.. _Learn Poshi section: https://qa-compendium.readthedocs.io/en/latest/poshi/index-poshi.html
.. _Forms test directory: https://github.com/liferay/liferay-portal/tree/master/portal-web/test/functional/com/liferay/portalweb/tests/enduser/webformsanddatalists/forms