# Use cases

There are a number of recurrent use cases that are worth mentioning:

## Creating Merchants

Creating Merchants is usually the first step in the setup process. As mentioned in the [previous](docs/introduction/01-welcome.md) section, Merchants go through an evaluation before obtaining credentials, and this process is offline and can be delayed over time.

In order to create the Merchant, and trigger the following evaluation process, you should send a POST request to the `/api/financial/merchant/` endpoint and provide all the information required. The expected data includes basic bio and professional details about the Merchant.

![create-merchant](../../assets/images/create-merchant.png)

### Request

```shell
curl --request POST \
     --url https://api.nemuru.com/api/financials/merchant/ \
     --header 'Content-Type: application/json' \
     --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjVhOTQzNZjk4ZjgwIn0...' \
     --data '{
              "id": "6fef65a6-1e5f-11e9-ab34-d662bd873d88",
              "merchant_first_name": "Manolo",
              "merchant_last_name": "Lopez",
              "merchant_phone_number": "+34626901301",
              "merchant_email": "pinturas.manolo@nemuru.com",
              "merchant_declared_business_type": "self-employed",
              "merchant_business_name": "Pinturas Manolo",
              "merchant_amount_of_employees": "0_3",
              "merchant_category": "other",
              "merchant_postal_code": "08025",
              "merchant_turnover": "0K_300K",
              "merchant_corporate_id_number": "B000012"
            }'
```

### Response

<!--
type: tab
title: Schema
-->
```yaml json_schema
type: object
properties:
  status:
    type: string
    enum:
      - status_pending_documents
      - status_documents_completed
      - status_pre_approved
      - status_asleep
      - status_suspended
      - status_banned
    example: status_documents_completed
    description: Current status
  payload:
    type: object
    properties:
      created_at:
        type: string
        format: date-time
        example: '2020-02-04T12:52:15+00:00'
        description: Created at
      updated_at:
        type: string
        format: date-time
        example: '2020-03-20T10:07:33+00:00'
        description: Updated at
      id:
        type: string
        format: uuid
        example: 6fef65a6-1e5f-11e9-ab34-d662bd873d88
        description: Id
      registration_fields:
        type: object
        properties:
          business_type:
            type: object
            required:
              - declared_business_type
              - business_type
            properties:
              declared_business_type:
                type: string
                description: The Merchant declared business type
                enum:
                  - self-employed
                  - ltd
                example: self-employed
              business_type:
                type: string
                description: The Merchant business type
                example: freelance
          email:
            type: string
            format: email
            example: pinturas.manolo@nemuru.com
            description: The Merchant email
          phone_number:
            type: string
            description: The Merchant phone number
            example: '+34626901301'
          full_name:
            type: object
            required:
              - first_name
              - last_name
            properties:
              first_name:
                type: string
                description: The Merchant first name
                example: Manolo
              last_name:
                type: string
                example: Lopez
                description: The Merchant last name
          business_name:
            type: string
            description: The Merchant business name
            example: Pinturas Manolo
          amount_of_employees:
            type: string
            description: The Merchant amount of employees
            enum:
              - '0_3'
              - '3_10'
              - '10_20'
              - 20_PLUS
            example: '0_3'
          category:
            type: string
            enum:
              - bathrooms
              - kitchen
              - whole_house
              - buildings
              - architecture
              - decoration_and_design
              - eco_improvement_and_solar_panels
              - real_estate_and_rentals
              - warehouse
              - painting
              - carpentry
              - home_staging
              - structure_and_humidity
              - installations
              - pools
              - elevators
              - awnings
              - gardening
              - other
              - cosmetic_surgery
              - travels
              - education_and_trainings
              - car_service
              - car_dealerships
            example: other
            description: The Merchant category
          postal_code:
            type: string
            example: '08025'
            description: The Merchant postal code
          turnover:
            type: string
            enum:
              - 0K_300K
              - 300K_1M
              - 1M_2M
              - 2M_5M
              - 5M_plus
            example: 0K_300K
            description: The Merchant turnover
          corporate_id_number:
            type: string
            description: The Merchant corporate id number
            example: 47865965K
        required:
          - business_type
          - email
          - phone_number
          - full_name
          - business_name
          - amount_of_employees
          - category
          - postal_code
          - turnover
          - corporate_id_number
      loan_programs:
        type: array
        description: The Merchant loan programs
        items:
          type: object
          properties:
            name:
              type: string
              enum:
                - free_program
                - zero_program
              example: free_program
              description: The Loan program
      segment:
        type: string
        enum:
          - super_diamond
          - diamond
          - platinum
          - gold
        example: gold
        description: The Merchant segment
      with_balance:
        type: boolean
        example: false
        description: Does the Merchant have a balance?
      cash_in_cash_out_method_ids:
        type: array
        description: The Merchant cash in cash out method ids
        items:
          type: string
          example: e1f2afb4-01b7-4251-9b7a-30d1ea2f4b44
      approval_status:
        type: object
        description: Approval status
        properties:
          is_approved_by_commercial:
            type: boolean
            example: true
            description: Is Merchant approved by Commercial?
          is_approved_by_risk:
            type: boolean
            example: true
            description: Is Merchant approved by Risk?
  identifier:
    type: string
    example: 'urn:nemuru:financial:merchant:6fef65a6-1e5f-11e9-ab34-d662bd873d88'
    description: The Merchant identifier
```
<!--
type: tab
title: Example
-->
```json
{
  "status": "ok",
  "payload": {
    "created_at": "2020-02-04T12:52:15+00:00",
    "updated_at": "2020-03-20T10:07:33+00:00",
    "id": "6fef65a6-1e5f-11e9-ab34-d662bd873d88",
    "registration_fields": {
      "full_name": {
        "first_name": "Manolo",
        "last_name": "Lopez"
      },
      "phone_number": "+34626901301",
      "email": "pinturas.manolo@nemuru.com",
      "business_type": {
        "business_type": "freelance",
        "declared_business_type": "self-employed"
      },
      "business_name": "Pinturas Manolo",
      "amount_of_employees": "0_3",
      "category": "other",
      "postal_code": "8025",
      "turnover": "0K_300K",
      "corporate_id_number": "B000012"
    },
    "status": "status_documents_completed",
    "approval_status": {
      "is_approved_by_commercial": true,
      "is_approved_by_risk": true
    },
    "cash_in_cash_out_method_ids": [
      "e1f2afb4-01b7-4251-9b7a-30d1ea2f4b44"
    ],
    "with_balance": false,
    "segment": "gold",
    "loan_programs": [
      {
        "name": "zero_program"
      },
      {
        "name": "free_program"
      }
    ]
  },
  "identifier": "urn:nemuru:financial:merchant:6fef65a6-1e5f-11e9-ab34-d662bd873d88"
}
```

<!-- type: tab-end -->



## Creating Loans

Creating a Loan is another very recurrent action. To create a Loan it will be necessary to provide two types of information: basic Loan parameters and contact details about the Borrower.

The corresponding endpoint is `/api/financial/loan/`.

![create-loan](../../assets/images/create-loan.png)

### Request

```shell
curl --request POST \
     --url https://api.nemuru.com/api/financials/merchant/ \
     --header 'Content-Type: application/json' \
     --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjVhOTQzNZjk4ZjgwIn0...' \
     --data '{
              "id": "e7c52ad3-0473-4fbc-bc36-7eb755b1c18d",
              "loan_conditions_currency": "EUR",
              "loan_conditions_user_conditions_term_period": "30.00",
              "loan_conditions_loan_calculator_principal": "8000.00",
              "loan_conditions_program": "free_program",
              "loan_conditions_fee_amount": "20.00",
              "merchant_id": "9286898b-7bb7-4885-9a9b-94c4e880378b",
              "borrower_invitation_email": "john.doe@nemuru.com",
              "borrower_invitation_first_name": "John",
              "borrower_invitation_last_name": "Doe",
              "borrower_invitation_phone_number": "+34601000001",
              "borrower_invitation_total_budget_amount": "10000.00",
              "borrower_invitation_job_description": "Reformas de mi casa"
            }'
```

### Response

<!--
type: tab
title: Schema
-->
```yaml json_schema
type: object
properties:
  created_at:
    type: string
    format: date-time
    example: '2020-03-23T12:33:55+00:00'
    description: Created at
  updated_at:
    type: string
    format: date-time
    example: '2020-03-23T12:33:55+00:00'
    description: Updated at
  id:
    type: string
    description: Id
    format: uuid
    example: 1c5d6380-13c3-44c0-930e-9ea9f6090559
  status:
    type: string
    description: The Loan status
    enum:
      - status_denied
      - status_desisted
      - status_expired
      - status_initial
      - status_lender_has_been_selected
      - status_active_trial
      - status_active
      - status_cancelled
      - status_analysing
      - status_contract_signed
      - status_docs_approved
      - status_unpaid
      - status_ended
    example: status_initial
```
<!--
type: tab
title: Example
-->
```json
{
    "created_at": "2020-03-23T12:33:55+00:00",
    "updated_at": "2020-03-23T12:33:55+00:00",
    "id": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
    "status": "status_initial",
    "loan_conditions": {
        "currency": "EUR",
        "due_date": "1",
        "program": {
            "name": "free_program",
            "merchant_discount_percentage": {
                "value": "0.0"
            }
        },
        "annual_interest": "0.075",
        "principal": {
            "currency": "EUR",
            "amount": "8000.0"
        },
        "loan_calculator": {
            "currency": "EUR",
            "setup_fee": {
                "type": "type_fixed_amount",
                "fee_amount": {
                    "currency": "EUR",
                    "amount": "8000.0"
                }
            },
            "term": {
                "period": "30.0",
                "type": "type_period",
                "interval": "P1M",
                "number_of_payments": "30"
            },
            "tae": "0.075",
            "total_interest_paid": {
                "currency": "EUR",
                "amount": "8000.0"
            },
            "total_amount_paid": {
                "currency": "EUR",
                "amount": "8000.0"
            },
            "user_defined_quota": {
                "currency": "EUR",
                "amount": "8000.0"
            }
        }
    },
    "borrowerId": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
    "borrower_invitation": {
        "email": "john.doe@nemuru.com",
        "full_name": {
            "first_name": "John",
            "last_name": "Doe"
        },
        "phone_number": "+34601000001",
        "borrower_invitation_expires_on": "2020-08-15T00:00:00+00:00",
        "total_budget": {
            "currency": "EUR",
            "amount": "10000.0"
        },
        "job_description": "Reformas de mi casa"
    },
    "borrower_user_details_on_origination": {
        "documentId": {
            "document_type": "nif",
            "document_expeditor": "ESP",
            "nationality": "ESP",
            "document_number": "48022321K",
            "expiration": "2026-11-17T11:19:05+00:00",
            "full_name": {
                "first_name": "John",
                "last_name": "Doe"
            },
            "birth_date": "1984-07-01T11:19:05+00:00",
            "gender": "M",
            "document_address": {
                "formatted_address": "Santa rosalia 153, P , Barcelona, Barcelona, Spain 08032",
                "geo_locate_provider_address": {
                    "street_number": "153",
                    "street_name": "Carrer de la farigola",
                    "city": "Barcelona",
                    "province_short_name": "Barcelona",
                    "province_long_name": "Barcelona",
                    "region_short_name": "CT",
                    "region_long_name": "Catalunya",
                    "country_short_name": "ES",
                    "country_long_name": "Spain",
                    "postal_code": 8032,
                    "geo_locate_provider_address": "Carrer de Santa Rosalia, 153, 08032 Barcelona, Spain",
                    "geo_locate_coordinates": {
                        "latitude": 41.4248456,
                        "longitude": 2.1512704
                    }
                }
            },
            "front_side_cloud_document": {
                "link_resource": "/document_id_front/1c5d6380-13c3-44c0-930e-9ea9f6090559.jpeg"
            },
            "back_side_cloud_document": {
                "link_resource": "/document_id_front/1c5d6380-13c3-44c0-930e-9ea9f6090559.jpeg"
            }
        },
        "familiar_situation_details": {
            "marital_situation": {
                "marital_status": "married",
                "marital_regime": "matrimonial_assets"
            }
        },
        "main_residence_details": {
            "address": {
                "formatted_address": "Santa rosalia 153, P , Barcelona, Barcelona, Spain 08032",
                "geo_locate_provider_address": {
                    "street_number": "153",
                    "street_name": "Carrer de la farigola",
                    "city": "Barcelona",
                    "province_short_name": "Barcelona",
                    "province_long_name": "Barcelona",
                    "region_short_name": "CT",
                    "region_long_name": "Catalunya",
                    "country_short_name": "ES",
                    "country_long_name": "Spain",
                    "postal_code": 8032,
                    "geo_locate_provider_address": "Carrer de Santa Rosalia, 153, 08032 Barcelona, Spain",
                    "geo_locate_coordinates": {
                        "latitude": 41.4248456,
                        "longitude": 2.1512704
                    }
                }
            },
            "ownership_details": {
                "property_type": "public_deed",
                "ownership_type": "ownership",
                "mortgage": true
            }
        },
        "professional_details": {
            "employment_status": "indefinite_employed",
            "company_info": {
                "activity": "commerce",
                "city": "Barcelona",
                "name": "John Doe",
                "seniority_months": 11,
                "seniority_years": 1
            },
            "professional_position": "technicians_and_professional"
        }
    },
    "borrower_bank_reader_id": "1c5d04a6-5f35-44b5-894a-84d40bc48d02",
    "borrower_cash_in_cash_out_method_id": "66ce223c-44ef-4b28-97bc-d51c1416ff21",
    "merchant_cash_in_cash_out_method_id": "e1f2afb4-01b7-4251-9b7a-30d1ea2f4b44",
    "merchant_id": "6fef65a6-1e5f-11e9-ab34-d662bd873d88",
    "loan_asset": {
        "work_site_address": {
            "formatted_address": "Santa Rosalia 153 1 1 Barcelona Barcelona España 08032",
            "geo_locate_provider_address": {
                "street_number": "153",
                "street_name": "Carrer de Santa Rosalia",
                "city": "Barcelona",
                "province_short_name": "Barcelona",
                "province_long_name": "Barcelona",
                "region_short_name": "CT",
                "region_long_name": "Catalunya",
                "country_short_name": "ES",
                "country_long_name": "Spain",
                "postal_code": 8032,
                "geo_locate_provider_address": "Carrer de Santa Rosalia, 153, 08032 Barcelona, Spain",
                "geo_locate_coordinates": {
                    "latitude": "41.4248456",
                    "longitude": "2.1512704"
                }
            }
        },
        "asset_type": "home_improvement",
        "status": "in_progress_status",
        "loan_asset_steps": [
            {
                "name": "Certificación inicial de obras",
                "amount_related": {
                    "currency": "EUR",
                    "amount": "4000"
                },
                "borrower_is_completed": "false",
                "certification_completed_date": "2019-03-01T11:19:05+02:00"
            }
        ],
        "total_pending_loan_asset_steps_amount": {
            "amount": "8000.0",
            "currency": "EUR"
        }
    },
    "origination_risk_values_id": "bef7cbea-3d26-4649-8c99-7fb3950bee8a",
    "lender_risk_values_id": "0092ae23-0136-4659-8487-9fb01e6cf7d3",
    "loan_application_ids": [
        "26df3bb2-410f-406b-9fb2-e5215d1e56c2"
    ],
    "loan_application_selected": {
        "created_at": "2020-03-23T12:33:55+00:00",
        "updated_at": "2020-03-23T12:33:55+00:00",
        "id": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
        "lender_fields": {
            "loan_application_status": {
                "state": "selected",
                "lender_approval_status": "null"
            },
            "lender_request_id": "43430f1c-d733-4bbe-a57a-7d5dcece25c1"
        },
        "merchant_id_in_lender_context": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
        "lender_id": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
        "loan_lender_borrower_contract": {
            "is_signed": "false",
            "signed_date": "2020-08-15T00:00:00+00:00",
            "is_sent": "false",
            "borrower_email": "nemuru@nemuru.com",
            "borrower_phone_number": "+34601000001",
            "loan_conditions": {
                "currency": "EUR",
                "due_date": "1",
                "program": {
                    "name": "free_program",
                    "merchant_discount_percentage": {
                        "value": "0.0"
                    }
                },
                "annual_interest": "0.075",
                "principal": {
                    "currency": "EUR",
                    "amount": "8000.0"
                },
                "loan_calculator": {
                    "currency": "EUR",
                    "setup_fee": {
                        "type": "type_fixed_amount",
                        "fee_amount": {
                            "currency": "EUR",
                            "amount": "8000.0"
                        }
                    },
                    "term": {
                        "period": "30.0",
                        "type": "type_period",
                        "interval": "P1M",
                        "number_of_payments": "30"
                    },
                    "tae": "0.075",
                    "total_interest_paid": {
                        "currency": "EUR",
                        "amount": "8000.0"
                    },
                    "total_amount_paid": {
                        "currency": "EUR",
                        "amount": "8000.0"
                    },
                    "user_defined_quota": {
                        "currency": "EUR",
                        "amount": "8000.0"
                    }
                }
            },
            "borrower_user_details_on_origination": {
                "documentId": {
                    "document_type": "nif",
                    "document_expeditor": "ESP",
                    "nationality": "ESP",
                    "document_number": "48022321K",
                    "expiration": "2026-11-17T11:19:05+00:00",
                    "full_name": {
                        "first_name": "John",
                        "last_name": "Doe"
                    },
                    "birth_date": "1984-07-01T11:19:05+00:00",
                    "gender": "M",
                    "document_address": {
                        "formatted_address": "Santa rosalia 153, P , Barcelona, Barcelona, Spain 08032",
                        "geo_locate_provider_address": {
                            "street_number": "153",
                            "street_name": "Carrer de la farigola",
                            "city": "Barcelona",
                            "province_short_name": "Barcelona",
                            "province_long_name": "Barcelona",
                            "region_short_name": "CT",
                            "region_long_name": "Catalunya",
                            "country_short_name": "ES",
                            "country_long_name": "Spain",
                            "postal_code": 8032,
                            "geo_locate_provider_address": "Carrer de Santa Rosalia, 153, 08032 Barcelona, Spain",
                            "geo_locate_coordinates": {
                                "latitude": 41.4248456,
                                "longitude": 2.1512704
                            }
                        }
                    },
                    "front_side_cloud_document": {
                        "link_resource": "/document_id_front/1c5d6380-13c3-44c0-930e-9ea9f6090559.jpeg"
                    },
                    "back_side_cloud_document": {
                        "link_resource": "/document_id_front/1c5d6380-13c3-44c0-930e-9ea9f6090559.jpeg"
                    }
                },
                "familiar_situation_details": {
                    "marital_situation": {
                        "marital_status": "married",
                        "marital_regime": "matrimonial_assets"
                    }
                },
                "main_residence_details": {
                    "address": {
                        "formatted_address": "Santa rosalia 153, P , Barcelona, Barcelona, Spain 08032",
                        "geo_locate_provider_address": {
                            "street_number": "153",
                            "street_name": "Carrer de la farigola",
                            "city": "Barcelona",
                            "province_short_name": "Barcelona",
                            "province_long_name": "Barcelona",
                            "region_short_name": "CT",
                            "region_long_name": "Catalunya",
                            "country_short_name": "ES",
                            "country_long_name": "Spain",
                            "postal_code": 8032,
                            "geo_locate_provider_address": "Carrer de Santa Rosalia, 153, 08032 Barcelona, Spain",
                            "geo_locate_coordinates": {
                                "latitude": 41.4248456,
                                "longitude": 2.1512704
                            }
                        }
                    },
                    "ownership_details": {
                        "property_type": "public_deed",
                        "ownership_type": "ownership",
                        "mortgage": true
                    }
                },
                "professional_details": {
                    "employment_status": "indefinite_employed",
                    "company_info": {
                        "activity": "commerce",
                        "city": "Barcelona",
                        "name": "John Doe",
                        "seniority_months": 11,
                        "seniority_years": 1
                    },
                    "professional_position": "technicians_and_professional"
                }
            },
            "cash_in_cash_out_method_account_holder_code": "ES94839483948934893433",
            "cash_in_cash_out_method_account_participation_level": "owner",
            "borrower_invitation_total_budget": {
                "currency": "EUR",
                "amount": "8000.0"
            },
            "borrower_job_description": "Reformas de mi casa",
            "loan_asset_worksite_address": {
                "formatted_address": "Santa Rosalia 153 1 1 Barcelona Barcelona España 08032",
                "geo_locate_provider_address": {
                    "postal_code": 8032,
                    "country_short_name": "ES",
                    "country_long_name": "Spain",
                    "region_short_name": "CT",
                    "region_long_name": "Catalunya",
                    "street_number": "153",
                    "street_name": "Carrer de Santa Rosalia",
                    "province_short_name": "Barcelona",
                    "province_long_name": "Barcelona",
                    "city": "Barcelona",
                    "geo_locate_provider_address": "Carrer de Santa Rosalia, 153, 08032 Barcelona, Spain",
                    "geolocation_coordinates": {
                        "latitude": "41.4248456",
                        "longitude": "41.4248456"
                    }
                }
            },
            "loan_id": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
            "merchant_corporate_id_number": "47865965K",
            "merchant_full_name": {
                "first_name": "Manolo",
                "last_name": "Lopez"
            },
            "merchant_non_unique_email": "pinturas.manolo@nemuru.com",
            "borrower_payment_due_date": "1"
        },
        "loan_id": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
        "insurance": "no",
        "merchant_group_id": "1c5d6380-13c3-44c0-930e-9ea9f6090559",
        "merchant_category": "other",
        "lender_pricing": {
            "code": "HD4",
            "version": "01",
            "expensesPaymentMethod": "no"
        },
        "net_income": {
            "annual_net_income": {
                "currency": "EUR",
                "amount": "8000.0"
            },
            "monthly_net_income": {
                "currency": {
                    "value": "EUR"
                },
                "amount": {
                    "value": "333.0"
                }
            }
        },
        "is_documentation_uploaded_to_lender": "false"
    },
    "borrower_cash_in_cash_out_method_account_number": "ES9404877295148852887468",
    "choose_loan_application_first_call": {},
    "loan_approval_status": "status_initial",
    "merchant_category": "other"
}
```
<!-- type: tab-end -->


## Checking Loan details

There are multiple ways to check the details and status of Loans.
* **GET** `/api/financial/loan/`
* **GET** `/api/financial/merchant/{merchantId}/loan/`