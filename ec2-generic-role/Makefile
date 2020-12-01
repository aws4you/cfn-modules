
APPLICATION ?= DefaultApp

ifdef AWS_REGION
	SOURCE_REGION ?= $(AWS_REGION)
else
	SOURCE_REGION ?= eu-central-1
endif

CLOUDFORMATION_TEMPLATE := ec2-generic-role.yaml
SUBMODULE := GenericEC2Role

all:
	@echo "****************************************************************************************"
	@echo "Create Generic EC2 role with a command"
	@echo
	@echo "  make create-app"
	@echo
	@echo "You can customize the run command with the next options for example"
	@echo
	@echo "  APPLICATION=MyApp AWS_REGION=us-west-2 make create-app"
	@echo
	@echo "There're next commands for the make: create-app, update-app, delete-app"
	@echo "****************************************************************************************"


create-app:
	aws cloudformation --region $(SOURCE_REGION) create-stack --stack-name $(APPLICATION)-$(SUBMODULE) \
		--capabilities CAPABILITY_IAM  \
		--parameters \
        	ParameterKey=Application,ParameterValue=$(APPLICATION) \
		--template-body file://./$(CLOUDFORMATION_TEMPLATE)

	aws cloudformation --region $(SOURCE_REGION) wait stack-create-complete --stack-name $(APPLICATION)-$(SUBMODULE)
	aws cloudformation --region $(SOURCE_REGION) describe-stacks --stack-name $(APPLICATION)-$(SUBMODULE)

update-app:
	aws cloudformation --region $(SOURCE_REGION) update-stack --stack-name $(APPLICATION)-$(SUBMODULE) \
		--capabilities CAPABILITY_IAM   \
		--parameters \
        	ParameterKey=Application,ParameterValue=$(APPLICATION) \
		--template-body file://./$(CLOUDFORMATION_TEMPLATE)

	aws cloudformation --region $(SOURCE_REGION) wait stack-update-complete --stack-name $(APPLICATION)-$(SUBMODULE)
	aws cloudformation --region $(SOURCE_REGION) describe-stacks --stack-name $(APPLICATION)-$(SUBMODULE)

delete-app:
	aws cloudformation --region $(SOURCE_REGION) delete-stack --stack-name $(APPLICATION)-$(SUBMODULE)
	aws cloudformation --region $(SOURCE_REGION) wait stack-delete-complete --stack-name $(APPLICATION)-$(SUBMODULE)

