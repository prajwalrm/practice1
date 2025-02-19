class MockRCAObject:
    def __init__(self, has_stamp=False, initial_stamp=None):
        self.rca_reason = initial_stamp
        self.has_stamp = has_stamp

        # Simulated fields with setValue() method
        self.QzDocsCaptureTime = self.MockField()
        self.SourceCreatedTime = self.MockField()
        self.TaskCreationAfterHours = self.MockField()
        self.ValidatorsOnTask = self.MockField()
        self.RcaStampField = self.MockField()  # Stores the RCA stamp

    def RcaStamp(self):
        """✅ Instead of returning a function, directly return the field object"""
        return self.RcaStampField  # This object supports setValue()

    def write(self):
        """Simulate writing to a database"""
        pass  

    class MockField:
        """A simple field class that supports setValue()"""
        def __init__(self):
            self.value = None

        def setValue(self, value):
            self.value = value
