public class ReportController {

    @AuraEnabled
    public static String sendReport(List<id> reportIds, String emailId){
        try{
            List<Messaging.EmailFileAttachment> attachment = new List<Messaging.EmailFileAttachment>();
            List<Report> reportList = [Select id,Name,DeveloperName from Report where id = :reportIds];
            
            if(reportlist.size() > 0){
                for(report r: reportlist){
                    String reportId = (string)r.id;
                    String reportName = (string)r.Name;
                    ApexPages.PageReference objPage = new ApexPages.PageReference('/servlet/PrintableViewDownloadServlet?isdtp=p1&reportId=' + reportId);
                    Messaging.EmailFileAttachment objMsgEmailAttach = new Messaging.EmailFileAttachment();
                    objMsgEmailAttach.setFileName(reportName + '.xls');
                    objMsgEmailAttach.setBody(objPage.getContent());
                    objMsgEmailAttach.setContentType('application/vnd.ms-excel');
                    attachment.add(objMsgEmailAttach);
                }
                Messaging.SingleEmailMessage email = new Messaging.SingleEmailMessage();
                email.setToAddresses(new String[]{emailId});
                email.setSubject('contact report from salseforce');
                email.setHtmlBody('<br/><br/> plese review contact detail report attachment.<br/><br/>');
                email.setFileAttachments(attachment);
                email.setuseSignature(false);
                messaging.sendEmail(new Messaging.SingleEmailMessage[]{email});
            }
            return 'Scusses';
        } 
        catch(exception e){
             return 'Failed';
        }
        
    }
}
