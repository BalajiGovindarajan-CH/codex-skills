Business Problem:

As a Product Manager I am looking to build 'Funding as a Service' global system. Today as a Merchat Service provider, ABC handles 1000's of merchants. ABC provides acquiring services for these merchants. As service provider, we provide scheme connectivity for merchants to take card payments. Then as part of daily settlement, clear and settle funds to merchants. This is normal process. But sometimes there is delay n getting settlement files due to various reasons, in these situations funding to merchants is delayed as well.

To overcome this a new system to be developed to provide resiliency. Aim is to settle funds to Merchnst even if there is delay in clearing and settlement from schemes to ABC. When the actual process is back up, ABC will reconcile against what is settled to merchaants. So merchants are not affacted due to system issues.

Host data Capture system to send files to Funding system. This will take the file, run some basic valiations- file format , header, trailer and has totals. 
Then enrich the files. Records in the files are consolidated by merchants. Each one identify funds to be settled for a merchant. Enrichment involves referring to Merchnat Master data (exposed via API) and getting details aboutmerchants and adding to records. Also there will be merchant hotlist exposed as API which needs to be referred and marker added to each mercnaht.

After this the merchant data has to be sent to approval. Operations user should be able to view the indivudal merchants, amount and approve or reject the funding requests. Approved requests should be consolidated and sent to payment gateway.
Payment gateway will apply some rues like if fundiing request for a merchant > 1 miilion, then use wire transfer else ACH. Basically produce two different payment rails to be used.
Within payment rails, merchant records has to be split based on beneficiary bank to which we need to send the files (i.e banks where the merchants hold their accounts). Each may have slight variations in format. 
Once the files are formatted and sent out, sytem should mark the state. Then will recrove the acknowledgement from banks which will be used to reconclie.
Reconciliation engine should reconclie each step of the process and finally at file level and merchant level what is funded.

Non functional requirement:
system should be built adopting cloud native, microservices archietcture.
Should be scalable horizontally. We could start with file volume of 50 k records but if i needi should be able to sclae to 10 million records. SLA for 50 k records processing is 5 minutes. 10 million is less than 20 minutes.
User should have visibility at file level - incoming request, approved, rejected and funded
Should be restarteble if the process fails. Say if it fails after enrihment, should be able to restart from failed step
Incoming files could be multiple formats. Generic framework should be developed to read the files based defined schema configuration and valdate.
All internal steps should be based on canocial layout.
Outgoing files should also driven by schema specific to bank needs and should be be driven adaptor pattern
AWS should be used for infrasture and other services like APi gateway, EKS, Aurora etc 

Currently the process is file driven, but archietcture should scale with minimal changes if we move event driven in future.
