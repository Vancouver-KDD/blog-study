# Google Apps Script For Startups

I want to share with you the potential of Google Apps Script, and how it can potentially increase your productivity almost limitlessely.

- Do you use any of the google serviecs such as Gmail, Google Sheet, Gmail, Calendar, etc, on a regular basis?
- Do you want to keep track of something on regular basis?
- Does your work involve tasks that needs to be done on a regular basis? or do you want to perform tasks on a regular basis?

If you answered yes to any of the questions above, I am sure you will benefit by continue reading.

## Introduction to Google Apps Script

Google Apps Script, to put it simply, is a script, normally JavaScript, that runs on the Google Cloud and can interact easily with Google Services as well as any of the third party APIs.

One of the beauty about Google Apps Script is its ability to [add custom menus, dialogs, and sidebars to Google Docs, Sheets, and Forms](https://developers.google.com/apps-script/overview).

World's most popular CMS is none other than Excel and Spreadsheet and are used by a whopping [750million to 2 billion people every month](https://askwonder.com/research/number-google-sheets-users-worldwide-eoskdoxav#:~:text=Google%20Suite%2C%20which%20includes%20Google,1.2%20billion%20monthly%20users%20globally.).

If you are a developer, you can increase productivity of your non-developers by empowering their Spread Sheet.

If you are a non-developer, you can get someone else to help you or even learn it yourself, as JavaScript is one of the easiest language to learn as a beginner.

## Getting Started

First things first, you will need Google Account. Then to Create your first Google Apps Script simply go to [Google Spread Sheets](https://docs.google.com/spreadsheets) -> Extentions tab -> Apps Script
This will take you directly to a new tab with editor where you can write JavaScript.

## Hello World Example

Change the code to following

    function myFunc() {
        return 'hello world'
    }

and ensure to save the code by pressing cmd/ctrl + s or 💾 icon in the toolbar.

Go back to your Spread Sheet, click one of the cell to select, and enter following inside fx (not the cell itself but the big input right above the column header)

    =myFunc()

If you see the cell replaced by hello world, you are successful, if not ensure your apps script was saved correctly without typo and you enter value into fx not the cell itself.

## Reading Parameters/Cells

Like all functions, you can also receive parameters, in this case data directly from other cells in the same sheet.
Change the script myFunc to following

    function myFunc(cell1, cell2) {
        return cell1 + ' ' + cell2
    }

This time, write "hello" to A1 and "world" to A2, and in A3 write in fx

    =myFunc(A1, A2)

If you see hello world, you are successful.

If you pass in a column as range such as

    =myFunc(A1:A3)

Your parameter input will be

    [A1,A2,A3]

If you pass in a row as range such as

    =myFunc(A1:C1)

Your parameter input will be

    [[A1, B1, C1]] // Notice array inside of array

If you pass in range of cells (A1:C3) you will get following array(s) as input parameter

    [[A1, B1, C1], [A2, B2, C2], [A3, B3, C3]]

## Populating Cells

Similar to reading values, returning single array populates columns, and 2d arrays populating both columns and rows.

For example, returning following from myFunc

    function myFunc() {
        return ['hello', 'world']
    }

will result in

    hello
    -----
    world

and following example

    function myFunc() {
        return [['a1','b1'], ['a2', 'b2']]
    }

will result in

    a1 | b1
    -------
    a2 | b2

## Read Data From Other Sources

Quite often, you need to also read data from other sources such as other Spread Sheets, Docs, or API.

### From API

    function myFunc() {
        const response = UrlFetchApp.fetch('https://example.com')
        Logger.log(response)
    }

⚠️ You may get a Authorization Required popup when executing your code. Simply click on "Review permissions" -> Choose your Google Account -> Advanced -> Go to xxx (unsafe) -> Allow

Then execute `myFunc` by Press "Run". (Ensure `myFunc` is selected in the dropdown)
See the html content from the example.com website printed in the `Execution log`.
If you are using API which fetch JSON, you can simply parse the JSON using `JSON.parse()`

### From other Spread Sheets

It is easy to read data from other Spread Sheets, given that your Google Account has access to it.
First open other SpreadSheet and write down its id

    https://docs.google.com/spreadsheets/d/1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ/edit#gid=1063355045

In this example, the id is `1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ`
The code to open the SpreadSheet is

    SpreadsheetApp.openById("1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ")

If you have multiple sheets, you can select right one by sheet's name

    SpreadsheetApp.openById("1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ").getSheetByName('Sheet2')

or by its gid by simply searching through all the sheets ([reference](https://stackoverflow.com/a/66154983/1183996)).

    SpreadsheetApp.openById("1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ").getSheets()
    const gid = '1063355045'
    const sheet = sheets.filter(sh=>sh.getSheetId()==gid)[0]

Reading a range works by using getRange and getValues

    SpreadsheetApp.openById("1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ").getRange("A1:D4").getValues()

Note that you can also select right Sheet by name using getRange

    SpreadsheetApp.openById("1k1y-NmFalwPkNiSZDEuNIdCvjyQQe-IBssszU07N9aQ").getRange("Sheet2!A1:D4").getValues()

⚠️ You may get a Authorization Required popup when executing your code. Simply click on "Review permissions" -> Choose your Google Account -> Advanced -> Go to xxx (unsafe) -> Allow

## Custom Menus

As mentioned above, ability to create custom menus will allow non-devs to easily execute specfic function directly from the Spread Sheet toolbar.

To create a custom menu, simply create a function called onOpen and a function for each item. ([reference](https://developers.google.com/apps-script/guides/menus))

    function onOpen() {
    var ui = SpreadsheetApp.getUi();
    // Or DocumentApp or FormApp.
    ui.createMenu('Custom Menu')
        .addItem('First item', 'menuItem1')
        .addSeparator()
        .addSubMenu(ui.createMenu('Sub-menu')
            .addItem('Second item', 'menuItem2'))
        .addToUi();
    }

    function menuItem1() {
    SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
        .alert('You clicked the first menu item!');
    }

    function menuItem2() {
    SpreadsheetApp.getUi() // Or DocumentApp or FormApp.
        .alert('You clicked the second menu item!');
    }

## Time-Driven Triggers

Another very useful feature of Apps Script is its ability to trigger function on a timely basis (also known as CRON jobs). This sort of feature is often hard to set up even as a developer.
However, as Google Apps Script developer, it only takes a minute.
In the Apps Scripts tab -> click on Triggers ⏱ on the left sidebar -> Add Trigger -> for Select event source, select Time-Driven -> interval can be as short as every minute, to as long as once a month or you can specify a datetime.

## Sharing Apps Script across your projects

It is often than not that you have multiple Spread Sheets you want to use same Apps Script code without duplicating the code itself. Luckily it is very easy to do. Simply go to ⚙️ Project Settings in Apps Script and copy the Script ID.
In Another Apps Script, in Editor tab, click + on the Libraries, and enter the Script ID. By pressing "Look Up" you can ensure you have the correct Script ID.

## Other Useful Functionalities

There are other very useful functionalities of Apps Script such as generating PDF and sending emails (including PDF attachments). This is very useful if you generate invoices using Google Spread Sheets.
I won't go into details into how to implement as Google has created a demo already.
https://developers.google.com/apps-script/samples/automations/generate-pdfs

## Limitations

There are some, but generous, limitations that you may run into when scaling your code. Click [HERE](https://developers.google.com/apps-script/guides/services/quotas#current_quotas) for latest limitations to Apps Script.
Most notable limitation is 90 minutes (or 6 hours for paid workspace), for a total trigger runtime per day, and 100 (1500 for paid workspace) email recipients per day.
