resource "okta_inline_hook" "test" {
  name    = "testAcc_replace_with_uuid"
  status  = "ACTIVE"
  type    = "com.okta.saml.tokens.transform"
  version = "1.0.2"

  channel = {
    type    = "HTTP"
    version = "1.0.0"
    uri     = "https://example.com/test1"
    method  = "POST"
  }
  auth = {
    key   = "Authorization"
    type  = "HEADER"
    value = "secret"
  }
}

resource "okta_app_saml" "test" {
  label                     = "testAcc_replace_with_uuid"
  sso_url                   = "https://google.com"
  recipient                 = "https://here.com"
  destination               = "https://its-about-the-journey.com"
  audience                  = "https://audience.com"
  subject_name_id_template  = "$${user.userName}"
  subject_name_id_format    = "urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress"
  response_signed           = true
  signature_algorithm       = "RSA_SHA256"
  digest_algorithm          = "SHA256"
  honor_force_authn         = false
  authn_context_class_ref   = "urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport"
  inline_hook_id            = okta_inline_hook.test.id

  depends_on = [
    okta_inline_hook.test
  ]
  attribute_statements {
    type         = "GROUP"
    name         = "groups"
    filter_type  = "REGEX"
    filter_value = ".*"
  }
}