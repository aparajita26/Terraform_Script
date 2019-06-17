# Terraform_Script
resource "ASGRP_1" "test" {
  name     = "ASGRP_1"
  strategy = "cluster"
}

resource "ASGRP_1" "bar" {
  name                      = "ASGRP_1"
  max_size                  = 1
  min_size                  = 1
  health_check_grace_period = 300
  health_check_type         = "EC2"
  desired_capacity          = 1
  force_delete              = true
  placement_group           = "${ASGRP_1.id}"
  launch_configuration      = "${ASGRP_1.LH_1.name}"
  vpc_zone_identifier       = ["${subnet-0b710816641aeebd7}"]

initial_lifecycle_hook {
    name                 = "LH_1"
    default_result       = "ABANDON"
    heartbeat_timeout    = 3600
    lifecycle_transition = "autoscaling:EC2_INSTANCE_LAUNCHING"

    notification_metadata =

}
