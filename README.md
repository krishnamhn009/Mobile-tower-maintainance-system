# Mobile-tower-maintainance-system

Design document (including architecture diagram , High level design , low level design etc.)



  and deployment document for Mobile tower maintenance system. The system should be able to



Requirements 



1) Authenticate Technicians
  Auth Methods
***********

bool Login(LoginDto login);
bool Logout(LoginDto login);

LoginDto
{
  userName: string,
  password:string
}


2) A technician should be able to close, register , reassign a maintenance  request.

  
MaintenaceRequest Methods
**************************
MaintenaceRequestDto RegisterMaintenceRequest(MaintenaceRequestDto request);
MaintenaceRequestDto CloseMaintenceRequest(MaintenaceRequestDto request);
MaintenaceRequestDto ReAssignMaintenceRequest(Guid maintenceRequestId,MaintenaceRequestDto maintenceRequest,Guid userId);
MaintenaceRequestDto GetMaintenceRequestDetails(Guid maintenceRequestId);
List<MaintenaceRequestDto> GetAllMaintenceRequestDetails(DateTime startDate,DateTime endDate,int pageNo,int pageSize);
  
  
  MaintenaceRequestDto
{
  maintenceRequestId:Guid,
  assignedTo:Guid,
  createdBy : Guid,
  complainMessage:string,
  location : string,
  time :string
  ....
}

3) Technician should be able to send / receive/ alerts and notifications
  
  For events ,event grid can be used..so if any request is modifed ..then event will be published and subscriber will be notified
  
  
Notification Methods
**************************
bool Send(MessageDto request);

MessageDto
{
  id:guid,
  sendTo : string,
  message: string
}


4) There should be a complete log track of the MR. The live updates should flow from technician to the corporate office.
  Here SignalR can be used.A hub can be created and register endpoint something like **/maintenceRequest** Amd implement subscriber for hub in client app. Client app will get live updates.


5) Reporting.
  Can build api endpoint that will pull maintence request data (in list) and return to consumer (client application).


6) Should be able to handle high volume of data and transactions,
   backend application should deploy as api..and each fucntionality should be exposed as endpoint.For this, we can add pagination in api endpoints.








