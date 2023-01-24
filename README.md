# Suitelet-1
Suitescript for creating a suitelet for freshers recruitment.

This is the 2nd branch. 
/**
* @NApiVersion 2.0
* @NScriptType Suitelet
*/
define(['N/email','N/runtime','N/ui/serverWidget','N/record','N/url','N/http','N/redirect','N/search'],function(email,runtime,serverwidget,record,url,http,redirect,search){
    //TASK-1 of suitelets.
    function onRequest(context){
        if(context.request.method==='GET'){
                        
       
var form=serverwidget.createForm({
    title:'FRESHER RECRUITMENT PROCESS'
});
//form.clientScriptModulePath='./trail pageClientScript.js';

form.addSubmitButton({
    label:'Submit'
});

form.addButton({
    id:'buttonid2',
    label:'Cancel'
    
});
form.addResetButton({
    
    label:'Reset'
    
});
//first fieldgroup
form.addFieldGroup({
    id : 'first',
    label : 'Candidate Information'
    
});


form.addField({
    id : 'custform1',
    type : serverwidget.FieldType.TEXT,
    label : 'customForm',
    container : 'first'
});
form.addField({
    id : 'custform2',
    type : serverwidget.FieldType.TEXT,
    label : 'Email ID',
    container : 'first'
});
form.addField({
    id : 'custform3',
    type : serverwidget.FieldType.TEXT,
    label : 'Mr/Ms',
    container : 'first'
});
form.addField({
    id : 'custform4',
    type : serverwidget.FieldType.TEXT,
    label : 'Name',
    container : 'first'
});
form.addField({
    id : 'custform5',
    type : serverwidget.FieldType.TEXT,
    label : 'Contact Number',
    container : 'first'
});
form.addField({
    id : 'custform6',
    type : serverwidget.FieldType.TEXT,
    label : 'College Name',
    container : 'first'
});
//adding 2nd field group
form.addFieldGroup({
    id : 'second',
    label : 'Aptitude Test Information'
    
});
form.addField({
    id:'apti1',
    type:serverwidget.FieldType.TEXT,
    label:'Aptitude Test Status-1',
    container:'second'
});
//adding 3rd field group
form.addFieldGroup({
    id : 'third',
    label : 'Coding Test Information'
    
});
form.addField({
    id:'coding1',
    type:serverwidget.FieldType.TEXT,
    label:'Coding Test Status',
    container:'third'
});
form.addField({
    id:'coding2',
    type:serverwidget.FieldType.TEXT,
    label:'Technical Test Status',
    container:'third'
});
//adding tabs

var tab1=form.addTab({
    id:'tab1id',
    label:'Personal_Details'
});
var tab2 = form.addTab({
    id: 'tab2id',
    label: 'Communication_Details'
});
//adding sub tabs to tab1
form.addField({
    id:'tab1field',
    type: serverwidget.FieldType.TEXT,
    label:'Position Applied',
    container:'tab1id'
});
form.addSubtab({
    id: 'subtab1id',
    label: 'Fresher',
    tab: 'tab1id'
});

form.addSubtab({
    id: 'subtab2id',
    label: 'Laterals',
    tab: 'tab1id'
});
form.addField({
    id: 'campuscode',
    type: serverwidget.FieldType.TEXT,
    label: 'Campus code',
    container: 'subtab1id'
});

form.addField({
    id: 'campustype',
    type: serverwidget.FieldType.TEXT,
    label: 'Campus Type',
    container: 'subtab1id'
});
form.addField({
    id: 'campuslocation',
    type: serverwidget.FieldType.TEXT,
    label: 'Campus Location',
    container: 'subtab1id'
});
form.addField({
    id: 'city',
    type: serverwidget.FieldType.TEXT,
    label: 'City',
    container: 'subtab1id'
});
form.addField({
    id: 'drivedate',
    type: serverwidget.FieldType.TEXT,
    label: 'Drive Date',
    container: 'subtab1id'
});
//SUBTAB 2 FIELDS
form.addField({
    id: 'transactionfield',
    type: serverwidget.FieldType.TEXT,
    label: 'Transaction History - Coming Soon',
    container: 'subtab2id'
});
var sublist = form.addSublist({
    id: 'sublistid',
    type: serverwidget.SublistType.INLINEEDITOR,
    label: 'Inline Sublist',
    tab: 'tab2id'
});
sublist.addButton({
    id: 'buttonId',
    label: 'Print ',
    functionName: '' // Add the function triggered on button click
});

// Sublist Fields
sublist.addField({
    id: 'datefieldid',
    type: serverwidget.FieldType.DATE,
    label: 'Date'
});

sublist.addField({
    id: 'productfieldid',
    type: serverwidget.FieldType.TEXT,
    label: 'Product'
});

sublist.addField({
    id: 'qtyfieldid',
    type: serverwidget.FieldType.INTEGER,
    label: 'Quantity'
});

sublist.addField({
    id: 'upfieldid',
    type: serverwidget.FieldType.CURRENCY,
    label: 'Unit Cost'
});

context.response.writePage(form);

        }
        
        
        else if(context.request.method==='POST'){
            var request=context.request;
            var nameOfStudent=request.parameters.custform4;
            var numberOfStudent=request.parameters.custform5;
            var cllgname=request.parameters.custform6;
            var eml=request.parameters.custform2;
            log.debug({
                title :'name',
                details : nameOfStudent
            });
            log.debug({
                title: 'number',
                details:cllgname
            });
            //here we are taking the data from the form and saving it in the lead list
            var newFeatureRecord = record.create({
                type:record.Type.LEAD,
                   
                isDynamic: true,
               });
            
            newFeatureRecord.setValue({
                fieldId:'companyname',
                value:nameOfStudent
            });
            newFeatureRecord.setValue({
                fieldId:'subsidiary',
                value:cllgname
            });
            newFeatureRecord.setValue({
                fieldId:'email',
                value:eml
            });
            newFeatureRecord.setValue({
                fieldId:'phone',
                value:numberOfStudent
            });
            var recordId=newFeatureRecord.save({
                enableSourcing:false,
                ignoreMandatoryFields:true
            });
            context.response.sendRedirect({
                type:http.RedirectType.RECORD,
                identifier:record.Type.LEAD,        
            });                       
        }
       
    }
    
    return{
        onRequest:onRequest
    };
});
