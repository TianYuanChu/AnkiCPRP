<?php 
	$datestring = "%y-%m-%d";
	$time = time();
	$dates = mdate($datestring, $time);
?>
<h1>Weekly Report</h1>
<?php echo form_open('report/send'); ?>
<fieldset>
	<legend id="title"><?php echo $title ?> </legend>
	<?php echo form_input(array(
									'name'=>'date',
									'value'=>$date
									));?>
</fieldset>
<fieldset>
	<legend id="current"><?php echo $lb_cur ?></legend>
		<?php echo form_label($lb_goals, 'goal');
			  echo form_textarea(array(
							'name'=>'goal',
							'cols'=>'32',
							'rows'=>'6',
							));?>
		<?php echo form_label( $lb_hrs, 'hours');
			  echo form_input(array(
									'name'=>'hours',
									'value'=>'10',
									'class'=>'hr'
									));?>
</fieldset>
<fieldset>
	<legend id="past" ><?php echo $lb_past ?></legend>
		<?php echo form_label($lb_ant, 'lw_ant');
			  echo form_textarea(array(
									'name'=>'lw_ant',
									'cols'=>'32',
									'rows'=>'6',
									));?>
		<?php echo form_label($lb_unt, 'lw_unt');
			  echo form_textarea(array(
									'name'=>'lw_unt',
									'cols'=>'32',
									'rows'=>'6',
									)
								);?>
		<?php echo form_label($lb_mis, 'lw_miss');
			  echo form_textarea(array(
									'name'=>'lw_mis',
									'cols'=>'32',
									'rows'=>'6',
									)
								);?>
</fieldset>
<fieldset>
	<legend id="issues" ><?php echo $lb_isu ?></legend>
		  <?php
		  echo form_textarea(array(
									'name'=>'issues',
									'cols'=>'32',
									'rows'=>'6',
									)
								);?>
</fieldset>
<fieldset>
	<legend id="schedule" ><?php echo $lb_sch ?></legend>
	<div class="blk">
	Mon: <?php echo form_input(array('name'=>'mon','class'=>'hr','value'=>'0')) ?>
	Tue: <?php echo form_input(array('name'=>'tue','class'=>'hr','value'=>'0')) ?>
	</div>
	<div class="blk">
	Wed: <?php echo form_input(array('name'=>'wed','class'=>'hr','value'=>'0')) ?>
	Thu: <?php echo form_input(array('name'=>'thu','class'=>'hr','value'=>'0')) ?>
	</div>
	<div class="blk">
	Fri: <?php echo form_input(array('name'=>'fri','class'=>'hr','value'=>'0')) ?>
	Sat: <?php echo form_input(array('name'=>'sat','class'=>'hr','value'=>'0')) ?>
	</div>
	Sun: <?php echo form_input(array('name'=>'sun','class'=>'hr','value'=>'0')) ?>
	Total: <?php echo form_input(array('name'=>'tol','class'=>'hr','value'=>'0')) ?>
</fieldset>
<fieldset>
	<legend>Notes</legend>
	<?php echo form_textarea(array('name'=>'note','cols'=>'32','rows'=>'6')) ?>
</fieldset>
<fieldset>
	<?php
	echo form_label('To:','to');
	echo form_input('to',$to);
	echo form_label('From: (Your email address)','from');
	echo form_input('from', $from);
	echo form_submit('submit', 'Send!');
	?>
	<?php echo validation_errors('<p class="error">'); ?>
</fieldset>

<br />
<?php if(isset($msg)):?>
	<?php echo $msg; ?>
<?php endif ?>

<?php
	if(isset($goals))
?>
