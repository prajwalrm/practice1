class MockRCAObject:
    def __init__(self, has_stamp=False, initial_stamp=None):
        self.QzDocsCaptureTime = self.MockField()
        self.SourceCreatedTime = self.MockField()
        self.TaskCreationAfterHours = self.MockField()
        self.ValidatorsOnTask = self.MockField()
        self._rca_stamp = initial_stamp  # Internal storage for RCA stamp value

    @property
    def RcaStamp(self):
        # Return a MockField-like object that supports both value retrieval and setting
        return self.RcaStampField(self)

    def write(self):
        pass  # Simulating a database write operation

    class MockField:
        def __init__(self, parent):
            self.parent = parent  # Reference to the parent MockRCAObject

        def setValue(self, value):
            print(f"Setting value: {value}")  # Debugging check
            self.parent._rca_stamp = value  # Update the internal storage

        def __call__(self):
            # When RcaStamp is called as a method, return the value
            return self.parent._rca_stamp

        def __repr__(self):
            # For debugging purposes
            return f"MockField(value={self.parent._rca_stamp})"
